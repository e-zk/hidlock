# hidlock
Scripts for OpenBSD's [hotplugd(8)](https://man.openbsd.org/hotplugd "hotplugd manual") that lock the X screen when a USB HID device is attached.

## about
--

## installation
First, enable hotplugd(8). As root, type:

	rcctl enable hotplugd

Then copy the `attach` and `detach` scripts included in this repo to `/etc/hotplugd/` (create the directory if it does not exist).

Finally, start hotplugd(8):

	rcctl start hotplugd

