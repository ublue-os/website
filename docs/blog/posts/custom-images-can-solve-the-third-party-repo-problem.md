---
date: 2023-05-03
authors: 
  - castrojo
links:
  - Setting yourself up for success before moving to Fedora Silverblue: https://www.ypsidanger.com/setting-yourself-up-for-success-before-moving-to-fedora-silverblue/
  - Also got hit with the Freeworld issue: https://www.reddit.com/r/Fedora/comments/136lf7j/also_got_hit_with_the_freeworld_issue/
  - What is "-freeworld": https://www.reddit.com/r/Fedora/comments/135u4zj/what_is_freeworld/
  - Update to fedora 38 gone wrong: https://www.reddit.com/r/Fedora/comments/135td6c/update_to_fedora_38_gone_wrong/
  - DNF wants to replace the mesa / Video codecs I just installed: https://www.reddit.com/r/Fedora/comments/134gzdp/dnf_wants_to_replace_the_mesa_video_codecs_i_just/
  - Will this dependency nightmare ever end: https://www.reddit.com/r/Fedora/comments/134i2ys/will_this_dependency_nightmare_ever_end/
  - Fedora 37 and the recent mesa-driver debacle: https://www.reddit.com/r/Fedora/comments/134bkol/fedora_37_and_the_recent_mesadriver_debacle/
---

# Custom Images can solve the "Third Party Repo" problem

Fedora's image-based variants are moving to OCI-based container images, which neatly solves third-party repository problems. 

Over the past few weeks there have been multiple version and syncing issues between Fedora and RPMFusion, a recommended repository for multimedia codecs. 

<!-- more --> 

## A Different Philosophy 

Universal Blue images are designed to be hands-off and automated, therefore many "getting started" guides and documentation will not apply to our images. 

Typically you're not "doing Linux stuff" like individual package management directly on the host and leveraging flatpaks and containers for your workloads.

This includes multimedia codecs, they are included out of the box and don't need further configuration.  

## We're still in the middle of a Model Shift

The idea of having repositories that you configure and use is part of the general Linux tradition. Breaking your computer with a PPA is a rite of passage!

Generally speaking trying to use your habits in an image-based system can lead to frustration and confusion. Unfortunately forums encourage users to use their Silverblue machine just like normal Fedora. Just replace `dnf install foo` with `rpm-ostree install foo` and things will be fine. 

The shift towards OCI images has made much of this complexity unnecessary for the end user, as we can now move the complexity to the server side instead of asking the end user client to figure out if RPMfusion is working that day. 

## Removing Toil

Fedora users recently had to deal with an issue where RPMFusion and the main repositories were not in sync, leading to [these kinds of errors](https://discussion.fedoraproject.org/t/gnome-login-screen-might-not-start-when-mesa-va-drivers-freeworld-from-rpmfusion-are-installed/81856). The sidebar on the left side of this page also has links to different problems people were having in r/fedora due to this issue.

If you were on a stock Silverblue or Kinoite image, you **still** had to deal with this issue because [the RPMFusion instructions](https://rpmfusion.org/Howto/OSTree) tell you to set up your computer this way! 

```
Last metadata expiration check: 1:41:42 ago on ma. 01. mai 2023 kl. 10.06 +0200.
Dependencies resolved.

 Problem 1: package mesa-va-drivers-freeworld-23.0.2-1.fc37.1.x86_64 requires mesa-filesystem(x86-64) = 23.0.2, but none of the providers can be installed
  - cannot install both mesa-filesystem-23.0.3-1.fc37.x86_64 and mesa-filesystem-23.0.2-2.fc37.x86_64
  - cannot install both mesa-filesystem-23.0.2-2.fc37.x86_64 and mesa-filesystem-23.0.3-1.fc37.x86_64
  - cannot install the best update candidate for package mesa-va-drivers-freeworld-23.0.2-1.fc37.1.x86_64
  - cannot install the best update candidate for package mesa-filesystem-23.0.2-2.fc37.x86_64
 Problem 2: package mesa-va-drivers-freeworld-23.0.2-1.fc37.1.i686 requires mesa-filesystem(x86-32) = 23.0.2, but none of the providers can be installed
  - cannot install both mesa-filesystem-23.0.3-1.fc37.i686 and mesa-filesystem-23.0.2-2.fc37.i686
  - cannot install the best update candidate for package mesa-va-drivers-freeworld-23.0.2-1.fc37.1.i686
  - cannot install the best update candidate for package mesa-filesystem-23.0.2-2.fc37.i686
 Problem 3: mesa-filesystem-23.0.2-2.fc37.i686 has inferior architecture
  - cannot install both mesa-filesystem-23.0.3-1.fc37.x86_64 and mesa-filesystem-23.0.2-2.fc37.x86_64
  - package mesa-dri-drivers-23.0.3-1.fc37.x86_64 requires mesa-filesystem(x86-64) = 23.0.3-1.fc37, but none of the providers can be installed
  - cannot install both mesa-filesystem-23.0.2-2.fc37.x86_64 and mesa-filesystem-23.0.3-1.fc37.x86_64
  - package mesa-vdpau-drivers-freeworld-23.0.2-1.fc37.1.i686 requires mesa-filesystem(x86-32) = 23.0.2, but none of the providers can be installed
  - cannot install the best update candidate for package mesa-vdpau-drivers-freeworld-23.0.2-1.fc37.1.i686
  - cannot install the best update candidate for package mesa-dri-drivers-23.0.2-2.fc37.x86_64

```

If you were on a Universal Blue image you did not have this problem because the integration of codecs and other packages happens in the build step **before** it gets to your computer.

## It's time to move on

The community still feels that adding third party repositories is _normal_ and _expected behavior_, even when this results in a broken installation! To make matters worse, Flathub provides nearly all the codecs and packages necessary for full hardware acceleration and multimedia support! Having the codecs on the image is useful, the system file manager usually needs them on the image to generate useful video thumbnails, and unfortunately Flathub's codecs don't solve this problem.

There are no correct instructions to layer RPMFusion properly on Fedora Silverblue and Kinoite because there is no way to guarantee that those repositories will be synchronized, a system set up this way will always be much less reliable than a custom image. 

## Images are better for users

What Universal Blue does is add an additional layer of protection by ensuring that a non-working image never makes it to your PC. The conflicting repo causes a [build failure](https://github.com/ublue-os/main/actions/runs/4736674877/jobs/8428174904). Your PC keeps the working image until the issue is resolved, then you get a new one, no dealing with repositories at all!


<script src="https://giscus.app/client.js"
        data-repo="ublue-os/base"
        data-repo-id="R_kgDOIlRXgw"
        data-category="Announcements"
        data-category-id="DIC_kwDOIlRXg84CTCvR"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="en"
        crossorigin="anonymous"
        async>
</script>

