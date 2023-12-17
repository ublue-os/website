---
render_macros: false
---

# Creating a minimal CI/CD setup for building OCI containers

!!! warning

    This guide assumes a small level of commitment to learning GitHub Actions and OCI, and some previous experience in adjacent things like Git and Linux.

This guide consists of some shallow instructions for setting up a repo and a fully documented bare-bones image build action that builds `Containerfile`s fed to it. This guide is useful if you want to learn the basics of the technologies Universal Blue relies on while building something for yourself.

To get started, create your repo. Once all that's done, create an empty file at `.github/workflows/build.yml`. Then in the root of the repo create a file called `Containerfile.myimage`.

To start with, you can populate the `Containerfile` with this example content.
```Dockerfile
# select silverblue-main as the base image
FROM ghcr.io/ublue-os/silverblue-main

# install wine on top
RUN rpm-ostree install wine 

# finalize the build
RUN rm -rf /tmp/* /var/* && ostree container commit 
```

Then study the following `build.yml` and copy it into your own, optionally pruning some excess lines of documentation from it.

{% raw %}
```yaml
name: build-image
on: # when the build should be run
  pull_request:
  schedule:
    - cron: '0 16 * * *' # 16:00 UTC everyday (30 min delay after 'nvidia' builds)
  push:
      branches:
        - "main" # only build the main branch
  workflow_dispatch: # allows you to manually trigger builds
env: # these variables are the same on all matrix builds
    IMAGE_REGISTRY: ghcr.io/${{ github.repository_owner }} # generates the registry-part of the OCI image URL

jobs:
  # this is where the action happens!
  build-and-push:
    name: Build and push image
    runs-on: ubuntu-22.04
    permissions: # 
      contents: read # required for reading the repo source code
      packages: write # required for publishing packages
      id-token: write # required for logging in to github
    strategy:
      fail-fast: false # stop GH from cancelling all matrix builds if one fails
      matrix: # all combinations of these variables are built
        # !!! This is the most important section
        # Here you decide what to build. 
        # For multi-image projects, it is common to only use one Containerfile
        # and use matrix variables to pick between major versions and desktop editions.
        # See https://github.com/ublue-os/main/blob/main/.github/workflows/build.yml#L21
        # This example uses this approach, because the variables of a build
        # are configurable in the Containerfile, and that is easier to grasp when starting out.
        containerfile: [Containerfile.myimage]
        
    steps: 
      # "Checks out" the repo, i.e. brings its contents to the build environment.
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Gather environment variables
        # The `IMAGE_NAME` is generated from the name of the Containerfile, it is the part after the dot.
        run: echo "IMAGE_NAME=$(echo ${{ matrix.containerfile }} | cut -d . -f 2)" >> $GITHUB_ENV

      # Generate some metadata for the OCI image.
      # This isn't strictly necessary, but index sites like artifacthub make use of these.
      # See example https://artifacthub.io/packages/search?org=ublue-os&sort=relevance&page=1
      # See list of labels in the OCI spec https://github.com/opencontainers/image-spec/blob/main/annotations.md
      - name: Image Metadata
        uses: docker/metadata-action@v4
        id: meta
        with:
          images: |
            ${{ env.IMAGE_NAME }}
          labels: |
            org.opencontainers.image.title=${{ env.IMAGE_NAME }}
            org.opencontainers.image.description=${{ env.IMAGE_NAME }} is my custom OS image.

      # Tags are used to select which version of an image to use.
      # For example, using `silverblue-main:latest` would mean always using the latest version,
      # and using `silverblue-main:39` would lock you to the 39-major version.
      # This is where the tags to build your image are generated.
      - name: Generate tags
        id: generate-tags
        shell: bash
        run: |
          TAGS=()

          if [[ "${{ github.event_name }}" == "pull_request" ]]; then
            # if this is a PR, add a pr number tag
            TAGS+=("pr-${{ github.event.number }}")
          else
            # if this isn't a PR, add the latest tag and a timestamp tag
            TAGS+=("$(date +%Y%m%d)")
            TAGS+=("latest")
          fi

          echo "Publishing with the following tags: "
          echo "${TAGS[*]}"
          
          echo "TAGS=${TAGS[*]}" >> $GITHUB_OUTPUT

      # Build image using Buildah action
      - name: Build Image
        id: build_image
        uses: redhat-actions/buildah-build@v2
        with:
          containerfiles: "./${{ matrix.containerfile }}" # select which containerfile to build
          image: ${{ env.IMAGE_NAME }} # names the built image
          tags: ${{ steps.generate-tags.outputs.TAGS }} # pulls in tags from previous step
          labels: ${{ steps.meta.outputs.labels }} # pulls in labels from previous step
          oci: false # don't use OCI metadata format instead of the Docker format (false by default)

      # Workaround for a bug where capital letters in your GitHub username make it impossible to push to GHCR.
      # https://github.com/macbre/push-to-ghcr/issues/12
      - name: Lowercase Registry
        id: registry_case
        uses: ASzc/change-string-case-action@v5
        with:
          string: ${{ env.IMAGE_REGISTRY }}

      # Push the image to GitHub Container Registry
      - name: Push To GHCR
        uses: redhat-actions/push-to-registry@v2
        id: push
        env: # set user and pass to use for logging in to GHCR
          REGISTRY_USER: ${{ github.actor }}
          REGISTRY_PASSWORD: ${{ github.token }}
        with:
          image: ${{ steps.build_image.outputs.image }} # pulls in the newly built image from previous step
          tags: ${{ steps.build_image.outputs.tags }} # pulls in tags from previous step
          registry: ${{ steps.registry_case.outputs.lowercase }} # pulls in lowercased image registry string from previous step
          username: ${{ env.REGISTRY_USER }}
          password: ${{ env.REGISTRY_PASSWORD }}

      # Login (required for signing) 
      - name: Login to GHCR
        uses: docker/login-action@v2
        if: github.event_name != 'pull_request' # signing disabled for PRs because PRs from outside repos wont have access to your signing secret
        run: |
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      # Install cosign (for signing)
      - uses: sigstore/cosign-installer@v3.2.0
        if: github.event_name != 'pull_request' # signing disabled for PRs because PRs from outside repos wont have access to your signing secret
        run: |

      # Finally, sign the container  
      - name: Sign container image
        if: github.event_name != 'pull_request' # signing disabled for PRs because PRs from outside repos wont have access to your signing secret
        run: |
        env:
          TAGS: ${{ steps.push.outputs.digest }} # hash of the new image, to make sure we sign the right one
          COSIGN_EXPERIMENTAL: false
          COSIGN_PRIVATE_KEY: ${{ secrets.SIGNING_SECRET }}
        run: |
          cosign sign -y --key env://COSIGN_PRIVATE_KEY ${{ steps.registry_case.outputs.lowercase }}/${{ env.IMAGE_NAME }}@${TAGS}
```
{% endraw %}

At this point, you will still notice your builds failing. To fix this, you need to set up container signing. Follow [step 3 in the manual repo setup guide](/tinker/setup/manual/#3-set-up-container-signing) to do this.

After these steps, your repo is set up, and you're ready to tinker and explore!  

You can try changing to a single-containerfile setup where your build matrix sets all the build arguments necessary, like maybe you want to build Nvidia and non-Nvidia or KDE and GNOME versions of the same images. Check out [the build.yml for ublue-os/main](https://github.com/ublue-os/main/blob/main/.github/workflows/build.yml), [Bazzite](https://github.com/ublue-os/bazzite/blob/main/.github/workflows/build.yml), and [Bluefin](https://github.com/ublue-os/bluefin/blob/main/.github/workflows/build.yml) for inspiration.

You might also want to get in-depth with the Containerfile/Dockerfile syntax, for that, check the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/). You'll at least want to know about [`FROM`](https://docs.docker.com/engine/reference/builder/#from), [`RUN`](https://docs.docker.com/engine/reference/builder/#run), [`COPY`](https://docs.docker.com/engine/reference/builder/#copy), and [`ARG`](https://docs.docker.com/engine/reference/builder/#arg). Also check out the Containerfiles in Universal Blue projects for inspiration.

When you get to the point that a lot of your Containerfile is just a big `RUN` statement, consider creating a `build.sh` script and running that instead.

To add proper signing support, look at [signing.sh](https://github.com/ublue-os/startingpoint/blob/template/config/scripts/signing.sh) in ublue-os/startingpont. You'll have to adapt the script a little, but it shows everything that you need to do to get it to work properly.