# Codecs

uBlue comes with packages to enable hardware acceleration for codecs, ensuring smooth and power-efficient playback right out of the box.

## Background

Hardware-accelerated codecs offload the work of video encoding and decoding from the CPU to specialized hardware in your computer, such as your graphics card. This allows for smoother video playback and reduces the strain on your CPU, resulting in more efficient use of your system resources.

VA-API is an open-source API for hardware-accelerated video processing that is widely used in Linux. It provides a standard interface for applications to access the video encoding and decoding capabilities of the graphics hardware. VA-API is supported by Intel and AMD (i)GPUs and uBlue includes the necessary packages to use it out-of-the-box.

For Nvidia graphics cards, there is no official support for VA-API. However, there is a community-made VAAPI driver for Nvidia called `nvidia-vaapi-driver`. It adapts the VAAPI APIs to Nvidia's proprietary APIs, enabling VA-API support for Nvidia graphics cards. Nvidia also provides the NVIDIA Video Codec SDK, which includes NVENC for video encoding and NVDEC for decoding. Some programs directly support this.

Regardless of your graphics hardware, uBlue includes the packages you need to enable Hardware-accelerated codecs using VA-API.

## How to check that hardware-accelerated codecs are properly detected

To check if hardware-accelerated codecs are being recognized by your system, you can use Firefox:

1. Open Firefox.
2. In the address bar, type `about:support` and press Enter.
3. Look for the section titled "Media"
4. If hardware-accelerated codecs are detected you should see `HW` listed next to some codecs. For example ![firefox-with-hw-codecs](https://user-images.githubusercontent.com/815081/229374952-a345de0c-fb2a-4f22-9de3-1c0a7184d1d0.png)

## (nvidia) How to check that hardware-accelerated codecs are in use

While playing or encoding a video, open a terminal and run `nvidia-smi dmon`. If the GPU codec is in use, there will be a positive value under the "dec" (decoder) or enc (encoder) columns. For troubleshooting, check the [nvidia page](/images/nvidia/).

## How to configure the Firefox flatpak to use hardware-accelerated codecs

The Firefox flatpak may require a small configuration change to enable hardware-accelerated codecs. Here's how to do it:

1. Open the Firefox flatpak. In a terminal run: `flatpak run org.mozilla.firefox`
2. type `about:config` in the address bar.
3. Accept the warning that appears.
4. Search for `media.ffmpeg.vaapi.enable`.
5. Set the value to **true**.
6. Restart firefox to apply the change.

Nvidia users will need to follow [additional steps](/images/nvidia/#video-playback).

## How to Install the `ffmpeg-full` Flatpak Runtime

If you're using flatpaks and want to ensure that your codecs are hardware-accelerated, you may want to install the `org.freedesktop.Platform.ffmpeg-full` runtime. This runtime enables flatpaks to use hardware-accelerated codecs. You may or may not need to do this because some flatpaks support this runtime but do not specify it as a dependency. If you're running a flatpak and you want to be sure, it's safe to just install this. This section will show you how to install the `org.freedesktop.Platform.ffmpeg-full` runtime on your system.

In a terminal, enter:

```bash
flatpak install org.freedesktop.Platform.ffmpeg-full
```

This command will ask you which version of the runtime you want to install. It's usually fine to pick the newest version, and you can install more than one version if needed. Once you've made your selection, the runtime will be downloaded and installed on your system.

To verify that the ffmpeg-full runtime has been installed correctly, you can run the following command in the terminal:

```bash
flatpak list --runtime | grep ffmpeg-full
```

This command should return the version(s) of the runtime that you installed.

To check what runtime version a certain program is currently running (i.e Firefox), enter in a terminal:

```bash
flatpak info --show-extensions org.mozilla.firefox | grep runtime
```

Ensure that you also get the ffmpeg-full version returned by the previous command.
