---
hide:
  - navigation
---

# Making your Own

1. Fork the ublue-os/base repo:
2. Ensure your [GitHub Actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository) and [GitHub Packages](https://docs.github.com/en/packages) are set up and enabled
3. Change the [image name in the action](https://github.com/ublue-os/base/blob/aab8078cfdc7d2354e057a0ca4771d3a53d2df4c/.github/workflows/build.yml#L14) to match what you want to call your image
   - Changing it to `IMAGE_NAME: beagles` will name the final image: `ghcr.io/yourusername/beagles` - so you'll likely want that to be your cool name instead of `base`
4. Generate a keypair
   - Install the [cosign CLI tool](https://edu.chainguard.dev/open-source/sigstore/cosign/how-to-install-cosign/)
   - Run `cosign generate-key-pair`
   - In your repository settings, under Secrets and Variables -> Actions
     - Create a new secret, make sure that you don't put a password on the key as this will be used by an action:
     ![image](https://user-images.githubusercontent.com/1264109/216735595-0ecf1b66-b9ee-439e-87d7-c8cc43c2110a.png)
     - Call it `SIGNING_SECRET` and then paste the contents of `cosign.key` into the field and save it. Be careful to make sure it's the .key file and not the .pub file. It should look like this:  
     ![image](https://user-images.githubusercontent.com/1264109/216735690-2d19271f-cee2-45ac-a039-23e6a4c16b34.png)
     - Copy the `cosign.pub` key into the root of your repository, replacing the key you got from here.
     - Copy the instructions from the verification section of this readme and make adjustments to your container url. This part is important, users must have a method of verifying the image. The linux desktop must not lag behind in cloud when it comes to supply chain security, so we're starting right from the start! (Seriously don't skip this part) 
5. Start making modifications to your Containerfile!
   - Change a few things and keep an eye on your Actions and Packages section of your repo, you'll generate a new image one every merge and additionally every day. 
   - Follow the instructions at the top of this repo but this time with the `ghcr.io/yourusername/beagles` url and then you'll be good to go!
   - Hang out in the [discussions forums](https://github.com/orgs/ublue-os/discussions) with others to share tips and get help, enjoy!
