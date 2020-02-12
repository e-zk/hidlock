# hidlock
Scripts for OpenBSD's [hotplugd(8)](https://man.openbsd.org/hotplugd "hotplugd manual") that lock the X screen when a USB HID device is attached.

## about
--

## installation
1. Enable hotplugd(8):

		rcctl enable hotplugd

2. Clone this repo.
3. As root, copy the `attach` and `detach` scripts to `/etc/hotplugd/` (create the directory if it does not exist).
4. Enable hotplugd(8):

		rcctl start hotplugd

