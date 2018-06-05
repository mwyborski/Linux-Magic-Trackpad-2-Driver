# Linux-Magic-Trackpad-2-Driver

This repository contains the linux hid-magicmouse driver with Magic Trackpad 2 support for Linux 4.17-rc7. For older kernels you might have to diff and backport.

The driver is tested in combination with the xf86-libinput and xf86-mtrack driver. 

The driver supports bluetooth and USB. To connect the Trackpad via bluetooth, it must be clicked once after it is turned on, then the Trackpad tries to reconnect to the last paired (and trusted) connection.

Please help to test this driver and report issues. 

# libinput
You can just use the standard xf86-libinput driver and configure it through your Windows-Manager-Settings. This driver works very well, but does not support three-finger-drag, but tap-to-drag.

# mTrack
An example configuration for mtrack can be found in:
```
usr/share/X11/xorg.conf.d/90-magictrackpad.conf 
```
This configuration supports tap-to-click, two-finger-scroll and three-finger-drag. Though scrolling is not as smooth as with xf86-libinput. It can be used as starting point for your own configuration. Make sure, that you have xf86-input-mtrack-git installed and it gets loaded. You find more information about the options here: https://github.com/p2rkw/xf86-input-mtrack

## DKMS

@adam-h made a DKMS which can be used for testing:

Setup/install with:

    sudo sh ./scripts/install.sh

Remove with:

    sudo sh ./scripts/remove.sh

Or just use regular `dkms` commands once you've added `./linux/drivers/hid`.


