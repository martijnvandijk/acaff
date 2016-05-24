acaff -- Airgapped/Asynchronous caff(1)
=======================================

`acaff` is a pair of simple scripts I wrote to help myself deal with keysigning
  with `caff(1)`, while keeping my primary keys on an airgapped machine.

It was originally written in early 2015, and whether the name means
  “airgapped caff” or “asynchronous caff” has been lost to time.

Credit goes to weasel (Peter Palfrader) for writing `caff` in the first place.


TL;DR
-----

On the networked computer:

	% mount  /mnt/usb
	% acaff  /mnt/usb 0x12345678 0x23456789 ...
	% umount /mnt/usb

On the airgapped computer:

	% mount  /mnt/usb
	% acaff  /mnt/usb
	% umount /mnt/usb

Back to the networked computer:

	% mount  /mnt/usb
	% tar -xf /mnt/usb/caff.tar.bz2 ~/.caff/
	% caff 0x12345678 0x23456789 ...
	It's time for the mail canon!


Design rationale
----------------

- Makes keysigning less unbearably annoying than it would otherwise be.
- Does *not* trust data coming from outside the airgapped machine.
- In particular, key verification is done on the airgapped machine.


Files
-----

`acaff`, both on the airgapped machine and the networked one, is called
  with a directory as first argument.  The files written in that directory
  on the networked machine should be available on the airgapped machine.

Typically, this would be the mountpoint of some removable storage (USB
  thumbdrive, SD card, floppy, SPI flash, ...).

These are the files that get written there:

	.
	├── keyids       # Space-separated list of key ids, written in the first stage
	├── pubs.asc     # ASCII-armored file containing those keys
	└── caff.tar.bz2 # Tarball of caff's state



TODOs/limits
------------

- [ ] The signatures exist in plaintext on the non-airgapped machine.
- [ ] Check for cross-platform compatibility.


License
-------

Released under the terms of the [ISC license](LICENSE.md).
