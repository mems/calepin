	~/Library/Application Support/MobileSync/Backup/

- [omvt-project/mvt: MVT is a forensic tool to look for signs of infection in smartphone devices](https://github.com/mvt-project/mvt) - Read data from backup as JSON (like contacts, browser history, SMS messages, attachments,  etc.) then check infection. [Check a Backup with mvt-ios - Mobile Verification Toolkit](https://mvt-docs.readthedocs.io/en/latest/ios/backup/check.html)
- [iphonebackupbrowser - iPhone Backup Browser - Google Project Hosting](https://code.google.com/p/iphonebackupbrowser/)
- https://github.com/isakkarlsson/iphonebackupbrowser-enhanced
- https://github.com/bschlenk/iPhone-Backup-Analyzer
- https://github.com/gkaiser/iosbackuputil

### Binary plists format `*.mdbackup`

`*.mdbackup` (Binary plists) contains sqlite3 files (names SHA1 hash of its path) : http://www.iphonebackupextractor.com/blog/2010/sep/15/what-are-all-files-iphone-backup/

```
/*
 HEADER
	magic number ("bplist")
	file format version

 OBJECT TABLE
	variable-sized objects

	Object Formats (marker byte followed by additional info in some cases)
	null	0000 0000
	bool	0000 1000			// false
	bool	0000 1001			// true
	fill	0000 1111			// fill byte
	int		0001 nnnn	...		// # of bytes is 2^nnnn, big-endian bytes
	real	0010 nnnn	...		// # of bytes is 2^nnnn, big-endian bytes
	date	0011 0011	...		// 8 byte float follows, big-endian bytes
	data	0100 nnnn	[int]	...	// nnnn is number of bytes unless 1111 then int count follows, followed by bytes
	string	0101 nnnn	[int]	...	// ASCII string, nnnn is # of chars, else 1111 then int count, then bytes
	string	0110 nnnn	[int]	...	// Unicode string, nnnn is # of chars, else 1111 then int count, then big-endian 2-byte uint16_t
 			0111 xxxx			// unused
	uid		1000 nnnn	...		// nnnn+1 is # of bytes
 			1001 xxxx			// unused
	array	1010 nnnn	[int]	objref*	// nnnn is count, unless '1111', then int count follows
 			1011 xxxx			// unused
 		   	1100 xxxx			// unused
	dict	1101 nnnn	[int]	keyref* objref*	// nnnn is count, unless '1111', then int count follows
 			1110 xxxx			// unused
 		   	1111 xxxx			// unused

 OFFSET TABLE
	list of ints, byte size of which is given in trailer
	-- these are the byte offsets into the file
	-- number of these is in the trailer

 TRAILER
	byte size of offset ints in offset table
	byte size of object refs in arrays and dicts
	number of offsets in offset table (also is number of objects)
	element # in offset table which is top level object

 */
```
