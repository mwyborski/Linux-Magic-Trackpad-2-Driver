robbi5 created a dkms package with the driver that is known to work with kernel 4.4.0-57-generic on Ubuntu 16.04 LTS: https://github.com/robbi5/magictrackpad2-dkms

# Linux-Magic-Trackpad-2-Driver

The driver for the Apple Magic Trackpad 2 can be found in my cloned linux repo:
https://github.com/robotrovsky/linux

USB Device ID is registered in:
```
drivers/hid/hid-ids.h
drivers/hid/hid-apple.c
drivers/hid/hid-core.c
```

The modified MacBookPro Touchpad driver is bcm5974:
```
drivers/input/mouse/bcm5974.c
```


See the first commit:
https://github.com/robotrovsky/linux/commit/7b50169c3a8948e67a67eb530b91117a7f5d9d5b

Future modifications will only affect bcm5974.c.

I used this driver in combination with the mtrack-driver, to make use of the multitouch feature (e.g. 2-finger-tap for right-click, etc):
https://github.com/BlueDragonX/xf86-input-mtrack

Right now the driver only works over USB. I submitted an official patch to linux-input:
http://www.spinics.net/lists/kernel/msg2551703.html

You might want to have a look at the discussion:
https://github.com/torvalds/linux/pull/332#issuecomment-298339763

