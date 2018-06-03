# Linux-Magic-Trackpad-2-Driver

This repository contains the linux hid-magicmouse driver with Magic Trackpad 2 support.

The driver is tested in combination with the xf86-mtrack driver. An example configuration can be found in:
```
usr/share/X11/xorg.conf.d/90-magictrackpad.conf 
```
This configuration supports tap-to-click, two-finger-scroll and three-finger-drag. It can be used as starting point for your own configuration. Make sure, that you have xf86-input-mtrack-git installed and it gets loaded.

The driver supports bluetooth and USB. To connect the Trackpad via bluetooth, it must be clicked once after it is turned on, then the Trackpad tries to reconnect to the last paired (and trusted) connection.

Please help to test this driver and report issues. 

TODO:
- test with xf86-libinput
- test with xf86-synaptics
