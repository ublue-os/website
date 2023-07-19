---
date: 2023-07-19
comments: true
authors: 
  - castrojo
links:
  - sigstore: https://www.sigstore.dev/
  - cosign: https://docs.sigstore.dev/cosign/overview/
  - bootc: https://github.com/containers/bootc
  - Introducing sigstore, Easy Code Signing and Verification for Supply Chain Integrity: https://security.googleblog.com/2021/03/introducing-sigstore-easy-code-signing.html
  - Why we’re excited about the Sigstore general availability: https://github.blog/2022-10-25-why-were-excited-about-the-sigstore-general-availability/
  - A New Tool Wants to Save Open Source From Supply Chain Attacks: https://www.wired.com/story/sigstore-open-source-supply-chain-code-signing/
  - Sigstore, An open answer to software supply chain trust and security: https://www.redhat.com/en/blog/sigstore-open-answer-software-supply-chain-trust-and-security
---

# Sigstore signed images are now here

Universal Blue images have traditionally [been signed](https://universal-blue.org/tinker/setup/manual/?h=cosign#3-set-up-container-signing) by cosign so that you as a user can verify that the image you're booted into is the same one we make in GitHub.

This involves checking the key manually:

```
git clone https://github.com/ublue-os/nvidia 
cosign verify --key nvidia/cosign.pub ghcr.io/ublue-os/kinoite-nvidia
```

When you rebase to a Universal Blue image, you might have noticed something: 

    rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/kinoite-nvidia:38

The `ostree-unverified-registry` section is something that we've had to use because we didn't have a way to run a signed image. You had to manually check the signature that we provide with cosign (as listed above). 

## Actions needed to move to signed images!

Thanks to the [upstream efforts in rpm-ostree](https://github.com/coreos/rpm-ostree/issues/4272), we can now run fully signed images directly. In order to do this you need to rebase to a signed image:

    rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/kinoite-nvidia:38

And then reboot.

Check the [images](/images) page for updated rebase commands for your system. You'll now be on a signed image and be good to go, `rpm-ostree` and `skopeo` will handle the rest.

## Upgrading from stock Fedora

The policies in stock Fedora don't support migrating to a signed Universal Blue image directly. For now we're recommending to [rebase to an unsigned image first](https://universal-blue.org/images/#preparing-to-rebase) to get the right policies and keys in place, and then rebasing using the `ostree-image-signed:docker://` snippet. If you have any ideas on how to make this smoother feel free to open a PR or file an issue!

# Conclusion and Thanks!

We've updated the documentation to refer to this new command. You can of course continue to run on an unsigned image, but we recommend getting that sigstore goodness all the way to your device. 

If you're sad about the URL becoming more complex, don't worry, soon it'll look like this: `bootc switch ghcr.io/ublue-os/kinoite-nvidia:38`. We'll let you know when that day arrives.

A huge shoutout to the sigstore and Fedora communities for their guidance and support. This is an important milestone for Universal Blue, one more requirement for moving out of beta is out of the way!
