## Screensharing on Wayland

Screen sharing on Wayland can often not work due to apps not using xdg-desktop-portal/PipeWire.

Fortunately we now have xwaylandvideobridge, which is a bridge between the app and xdg-desktop-portal to allow apps to screen share, even when they don't directly support xdg-desktop-portal.

Only uBlue Kinoite has xwaylandvideobridge installed by default, since GNOME and wlroots have various issues with it.

Kinoite user can run ```just fixscreenshare``` for enabling Xwaylandvideobridge at startup