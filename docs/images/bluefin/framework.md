## Framework Images

Bluefin is available as an image for the Framework 13 laptop that comes preconfigured with tlp and the [recommended power settings](https://github.com/ublue-os/bluefin/blob/main/framework/etc/tlp.d/50-framework.conf) from the [Framework Knowledge Base](https://knowledgebase.frame.work/en_us/optimizing-fedora-battery-life-r1baXZh)

Note that the default image works fine on the Framework 13, this image provides tweaks and further improvements. Additionally if you have power profiles that you think would be useful for the community please send a pull request! 

1. Rebase to the -framework image: 

    Bluefin:

        sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-framework:38

    Bluefin Developer Experience:

        sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx-framework:38

1. Reboot! 
1. Then run this command to set the right kernel arguments for the brightness keys to work:
  
       just framework-13

Then reboot one more time and you're done!