acaff -- Airgapped/Asynchronous caff(1)
=======================================

`acaff` is a pair of simple scripts I wrote to help myself deal with keysigning
  with `caff(1)`, while keeping my primary keys on an airgapped machine.

It was originally written in early 2015, and whether the name means
  “airgapped caff” or “asynchronous caff” has been lot to time.

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


Rationale
---------

- Makes keysigning less unbearably annoying than it would otherwise be.
- Does *not* trust data coming from outside the airgapped machine.
- In particular, key verification is done on the airgapped machine.


TODOs/limits
------------

- [ ] The signatures exist in plaintext on the non-airgapped machine.
- [ ] Check for cross-platform compatibility.


License
-------

Released under the terms of the [ISC license](LICENSE.md).
