# Update 2019-04-19
Installed today Xubuntu 19.04 and the pressure problem was back. I had to add the following file:

```/usr/share/X11/xorg.conf.d/90-magictrackpad.conf```

```
Section "InputClass"
  Identifier      "Touchpads"
  Driver          "libinput"
  MatchProduct    "Apple Inc. Magic Trackpad 2"
  MatchDevicePath "/dev/input/event*"
EndSection
```

To pair via Bluetooth disconnect from USB, then turn it off and on again and you will find it when you search for devices.



# Update 2019-04-10
Tried today the beta of Ubuntu 19.04 with Kernel 5.0 and the Magic Trackpad 2 works out of the box. No quirks needed.

# Update 2019-01-07

As the pressure offsets have been removed from the official release, the driver needs a libinput quirks file. schmunk42 suggested the following quirks file in his comment https://github.com/torvalds/linux/pull/332#issuecomment-451859484:

```/etc/libinput/local-overrides.quirks```

    [Touchpad touch override]
    MatchUdevType=touchpad
    MatchName=*Magic Trackpad 2
    AttrPressureRange=4:0



# Update 2018-12-15

The driver will be included in the 4.20 release of the official linux kernel.

This means that the active development in this repository is stopped and you should use the official code for modifications.



## Thanks
* Thank you to everybody who helped, whether through testing or active development!
* https://github.com/bobbysue/Linux-Magic-Trackpad-2-Driver
* https://github.com/ponyfleisch/hid-magictrackpad2
* https://github.com/adam-h/Linux-Magic-Trackpad-2-Driver



# Linux-Magic-Trackpad-2-Driver

This repository contains the linux hid-magicmouse driver with Magic Trackpad 2 support for Linux 4.18. For older kernels you might have to diff and backport.

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
or for Ubuntu

    tail -f /var/log/Xorg.0.log

Now unplug the trackpad and plug it back in, to see which driver gets loaded.


