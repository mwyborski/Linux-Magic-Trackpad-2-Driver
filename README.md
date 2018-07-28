# Linux-Magic-Trackpad-2-Driver

This repository contains the linux hid-magicmouse driver with Magic Trackpad 2 and Magic Mouse 2 support for Linux 4.18. For older kernels you might have to diff and backport.

This driver is based off of the work of @robotrovsky, @svartalf and probably others.

The driver is tested in combination with the xf86-libinput and xf86-mtrack driver. 

The driver supports bluetooth and USB. To connect the Trackpad via bluetooth, it must be clicked once after it is turned on, then the Trackpad tries to reconnect to the last paired (and trusted) connection.

Please help to test this driver and report issues. 

## libinput
You can just use the standard xf86-libinput driver and configure it through your Window-Manager-Settings. This driver works very well, but does not support three-finger-drag, but tap-to-drag.

## mTrack
An example configuration for mtrack can be found in:
```
usr/share/X11/xorg.conf.d/90-magictrackpad.conf 
```
This configuration supports tap-to-click, two-finger-scroll and three-finger-drag. Though scrolling is not as smooth as with xf86-libinput. It can be used as starting point for your own configuration. Make sure, that you have xf86-input-mtrack-git installed and it gets loaded. You find more information about the options here: https://github.com/p2rkw/xf86-input-mtrack

## DKMS

@adam-h made a DKMS which can be used for testing:

Setup/install with:

    cd scripts
    sudo ./install.sh

Remove with:

    sudo ./remove.sh

Or just use regular `dkms` commands once you've added `./linux/drivers/hid`.

## Troubleshooting
If the driver is not working, please make sure that the correct hid-magicmouse driver gets loaded and try the following steps:

    cd linux/drivers/hid
    make
    sudo rmmod hid_magicmouse
    sudo insmod ./hid-magicmouse.ko
    tail -f ~/.local/share/xorg/Xorg.0.log

Now unplug the trackpad and plug it back in, to see which driver gets loaded.

## Thanks
* https://github.com/ponyfleisch/hid-magictrackpad2
* https://github.com/adam-h/Linux-Magic-Trackpad-2-Driver
* https://github.com/bobbysue/Linux-Magic-Trackpad-2-Driver
* https://github.com/svartalf/hid-magicmouse2
