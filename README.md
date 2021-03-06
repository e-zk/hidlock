# hidlock
`attach` and `detach` scripts for OpenBSD's [hotplugd(8)](https://man.openbsd.org/hotplugd) that lock all running X displays when a USB [HID](https://en.wikipedia.org/wiki/Human_interface_device) is attached.

![xlock running after HID attack detected](preview.png)
_Note: xlock formatting may vary accross systems_

## about
Human Interface Devices (HIDs) are input devices that allow humans to interface with computers. The most common HID used are keyboards and mice. A HID attack involves a malicious actor connecting a USB device into a target computer, and this USB device registering itself as a keyboard to the kernel, then playing back preconfigured keyboard keypresses in order to expose backdoors, change settings, and/or install programs - whatever a hacker can do with his hands on your keyboard, a malicious HID can (within reason). There are many platforms used for HID attacks, here are some of the more common ones:

* [USB RubberDucky (hak5)](https://shop.hak5.org/products/usb-rubber-ducky-deluxe)
* [Teensy](https://www.pjrc.com/) boards are also [commonly](https://www.cyberpointllc.com/posts/cp-human-interface-device-attack.html) [used](https://www.irongeek.com/i.php?page=security/programmable-hid-usb-keystroke-dongle)

These scripts aim to protect users somewhat from HID attacks by immediately locking running X displays when a HID is attached; this means that whatever keystrokes a malicious actor wants to execute are hooked into [xlock(1)](https://man.openbsd.org/xlock)'s password input instead of anywhere near running programs.

## installation
1. To enable hotplugd(8); as root type:

		rcctl enable hotplugd

2. Copy the `attach` and `detach` scripts included in this repo to `/etc/hotplug/` (create the directory if it does not exist):

		mkdir -p /etc/hotplug
		cp -iv attach detach /etc/hotplug
		
		# (optional) make sure the scripts are executable
		chmod +x /etc/hotplug/*

3. For xlock(1) to work properly, it has to be called by the user of the X display; to do this [doas(1)](https://man.openbsd.org/doas) can be used, provided the following rule is included in `/etc/doas.conf`:

		# note: this allows the root user to execute any command as any user without password confirmation
		permit nopass keepenv root

4. Finally, restart hotplugd(8):

		rcctl restart hotplugd

## todo / roadmap
* Makefile/install script for easier installation 
* Support for other lock programs 
