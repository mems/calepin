Install order

1. gettext
2. libusb
3. sane-backends
4. Twain Sane Interface

Run

	scaneimage -L

If not found, add to `/usr/local/etc/sane.d/canon_dr.conf`:

	option vendor-name  CANON
	option model-name   DR-C125
	option version-name XXXX
	usb 0x1083 0x1640

Now `scaneimage -L` returns something like:

	device `canon_dr:libusb:003:011-1083-1640-00-00' is a CANON DR-C125 scanner

`/Library/Image Capture`