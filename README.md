# hidlock
`attach` and `detach` scripts for OpenBSD's [hotplugd(8)](https://man.openbsd.org/hotplugd "hotplugd manual") that lock the X screen when a USB [HID](https://en.wikipedia.org/wiki/Human_interface_device "Human Interface Device (Wikipedia)") is attached.

## about
Human Interface Devices (HIDs) are input devices that allow humans to interface with computers, these include keyboards and mice. A HID attack involves a malicious actor connecting a USB device into a target computer, and this USB device playing back preconfigured keyboard keypresses in order to expose backdoors, change settings, and/or install programs. Here are a few common platforms used for HID attacks: 

* [USB RubberDucky (hak5)](https://shop.hak5.org/products/usb-rubber-ducky-deluxe)
* [Teensy](https://www.pjrc.com/ "PJRC Homepage") boards are also [commonly](https://www.cyberpointllc.com/posts/cp-human-interface-device-attack.html) [used](https://www.irongeek.com/i.php?page=security/programmable-hid-usb-keystroke-dongle)

These scripts aim to protect users somewhat from HID attacks by immediately locking running X displays when a HID is attached; this means that whatever keystrokes a malicious actor wants to execute are hooked into xlock(1)'s password input instead of anywhere near running programs.

## installation
First, enable hotplugd(8). As root, type:

	rcctl enable hotplugd

Then copy the `attach` and `detach` scripts included in this repo to `/etc/hotplugd/` (create the directory if it does not exist).

Finally, start hotplugd(8):

	rcctl start hotplugd

