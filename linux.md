systemd
-------

[It's FOSS - How to Check if Your Linux System Uses systemd](https://itsfoss.com/check-if-systemd)

[Linux Handbook - Using systemctl Command](https://linuxhandbook.com/systemctl-commands)

```Sh
# To see a summary of the time taken to boot, use
systemd-analyze

# To get a detailed breakdown of the time taken by each stage of the boot process, use
systemd-analyze blame

# To create a graphical representation of the boot process, use
systemd-analyze plot > boot_chart.svg

# To check the time taken by each systemd service to start, use
systemd-analyze critical-chain
systemd-analyze critical-chain ssh.service

# To display the current hostname and related information
hostnamectl

# To display current locale and keyboard settings
localectl status

# To set the system locale as American English
sudo localectl set-locale LANG=en_US.UTF-8

# To set the keyboard layout as the US keyboard layout
sudo localectl set-keymap us

# To display current time and date settings
timedatectl

# To list all current user sessions
loginctl list-sessions

```

Utilities
---------

### CLI

- neofetch
- inxi (full featured system information script)
- ncdu (ncurses disk usage viewer)
- gparted (GNOME partition editor)
- tldr
- mediainfo

### GUI

- obs-studio
- audacity


Modern Linux Graphics Stack 
---------------------------

[Wikipedia - Direct Rendering Infrastructure](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure)

[Wikipedia - Direct Rendering Manager](https://en.wikipedia.org/wiki/Direct_Rendering_Manager)

[知乎 - GPU渲染之路：从图形引擎到内核驱动](https://zhuanlan.zhihu.com/p/649971173)

[CSDN - DRM（Direct Rendering Manager）学习简介](https://blog.csdn.net/hexiaolong2009/article/details/83720940)



Linux on the Desktop
====================


Desktop Environment
-------------------

Install KDE Plasma on Ubuntu 24.04

``` Sh
sudo apt update
# sudo apt install kde-standard
sudo apt install kde-full
```

Switch display manager

``` Sh
sudo dpkg-reconfigure gdm3
```

[Wikipedia - X display manager](https://en.wikipedia.org/wiki/X_display_manager)

[Wikipedia - GNOME Display Manager](https://en.wikipedia.org/wiki/GNOME_Display_Manager)

[Wikipedia - Simple Desktop Display Manager](https://en.wikipedia.org/wiki/Simple_Desktop_Display_Manager)


[StackExchange - Is there a way to get list of windows on KDE Wayland?](https://unix.stackexchange.com/questions/706477/is-there-a-way-to-get-list-of-windows-on-kde-wayland)

``` Sh
wmctrl -l # list X11 windows on XWayland
```

https://en.wikipedia.org/wiki/Linux_range_of_use#Desktop

https://pointieststick.com/2023/12/26/does-wayland-really-break-everything

https://blog.tenstral.net/2024/01/wayland-really-breaks-things-just-for-now.html

https://itsfoss.com/gnome-screen-recorder

https://itsfoss.com/screen-record-obs-wayland

https://pointieststick.com/2023/09/17/so-lets-talk-about-this-wayland-thing


X11
---

### wmctrl

``` Sh
wmctrl -n $(($(wmctrl -d | wc -l) + 1)) # Create new workspace
wmctrl -s $(($(wmctrl -d | wc -l) - 1)) # Switch to the new workspace
wmctrl -d # Verify the current workspace
```


D-Bus
-----

https://dbus.freedesktop.org/doc/dbus-tutorial.html

[Wikipedia - D-Bus](https://en.wikipedia.org/wiki/D-Bus)

[ArchWiki - D-Bus](https://wiki.archlinux.org/title/D-Bus)

D-Bus debugger GUI tools: [D-Spy](https://apps.gnome.org/en/Dspy)

Implementations: [sdbus-cpp](https://github.com/Kistler-Group/sdbus-cpp)

```bash
# Ubuntu
sudo apt install libsdbus-c++-dev
pkg-config --list-all | grep sdbus
```

XDG Desktop Portal
------------------

[ArchLinux - XDG Desktop Portal](https://wiki.archlinux.org/title/XDG_Desktop_Portal)

[ArchLinux - XDG Base Directory](https://wiki.archlinux.org/title/XDG_Base_Directory)

[ArchLinux - XDG user directories](https://wiki.archlinux.org/title/XDG_user_directories)


### [ScreenCast](https://flatpak.github.io/xdg-desktop-portal/docs/doc-org.freedesktop.impl.portal.ScreenCast.html)


```
CreateSession(Vardict options)->(Object Path handle)
SelectSources(Object Path session_handle, Vardict options)->(File Descriptor fd)
Start(Object Path session_handle, string parent_window)->(Object Path handle)
OpenPipeWireRemote(Object Path session_handle, Vardict options)->(Object Path handle)

CreateSession->SelectSources->Start->OpenPipeWireRemote
```

Python examples

[GNOME GitLab - Using XDG Desktop Portal Screencast to record screen/window](https://gitlab.gnome.org/-/snippets/19)

[A simple, configurable screen recorder for Wayland (XDG portal) with a terminal interface](https://github.com/afontenot/pipewire-screencast)


[Kooha](https://github.com/SeaDve/Kooha)


PipeWire
--------

https://docs.pipewire.org/page_tutorial4.html

https://docs.pipewire.org/page_tutorial5.html

https://wiki.archlinux.org/title/PipeWire

https://docs.pipewire.org

https://github.com/PipeWire/pipewire

https://github.com/mikeroyal/PipeWire-Guide

https://blogs.gnome.org/uraeus/2021/10/01/pipewire-and-fixing-the-linux-video-capture-stack

https://discourse.gstreamer.org/t/gstreamer-and-pipewire/3586


### Runtime

XDG Desktop Portal

```bash
dpkg -l | grep xdg-desktop-portal
systemctl --user status xdg-desktop-portal.service
systemctl --user status xdg-desktop-portal-gnome.service
systemctl --user status xdg-desktop-portal-gtk.service
```

PipeWire

```bash
dpkg -l | grep wireplumber
dpkg -l | grep pipewire
systemctl --user status wireplumber
systemctl --user status pipewire
```

gstreamer-plugin-pipewire

```bash
dpkg -l | grep gstreamer
gst-inspect-1.0 pipewire
gst-inspect-1.0 pipewiresrc
```


APUE
----

Standard IO: portable, bufferd

Process terminates normally,
- return from main()
- call exit(), _exit(), _Exit()

Process terminates normally,
- abort()
- signal