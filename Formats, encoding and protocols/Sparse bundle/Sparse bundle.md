> While both sparse images and sparse bundles contain a file system, a sparse bundle is bundle-backed, meaning that it employs a specialized, hierarchical directory structure for grouping related resources. Within a sparse bundle, the bands subdirectory contains the actual data saved within the disk image. 

- [SparseBundle.c](http://opensource.apple.com//source/hfs/hfs-305.10.1/CopyHFSMeta/SparseBundle.c)
- [How to fix a Corrupted Time Machine Backup | Jthon's Place](http://blog.jthon.com/?p=31)
- [osx - can sparsebundles be locked to make them read-only? - Super User](http://superuser.com/questions/543388/can-sparsebundles-be-locked-to-make-them-read-only)
- [How to Use Mac OS X Sparse Bundle Disk Images - Stephen Foskett, Pack Rat](http://blog.fosketts.net/2015/07/22/how-to-use-mac-os-x-sparse-bundle-disk-images/)
- [Sparse image — Wikipedia](https://en.wikipedia.org/wiki/Sparse_image)
- [Bundle (OS X) — Wikipedia](https://en.wikipedia.org/wiki/Bundle_(OS_X))

Change band size:

	hdiutil convert -format UDSB -imagekey sparse-band-size=262144 -o new.sparsebundle old.sparsebundle
	# Will take lot of time ~ hours

> The sparse-band-size parameter is the number of 512-byte sectors (chunks), not the number of bytes. Since 512 is 1/2 1,024, then 262,144 B / 2 = 128 KiB.

Where 262144 equals 128MB bands/byte sectors (`128 MBytes == 128*1024*1024 bytes == 128*1024*1024/512 blocks = 262144 blocks`, `262144 / 2 / 1024 = 128MB`)

Read it:

	hdiutil info -verbose | grep band-size
	# Or accessible in Info.plist in the .sparsebundle

- [Apple's Time Machine fuse read only file system](https://github.com/abique/tmfs)
- [Can Linux mount a normal Time Machine sparse bundle disk image directory? - Super User](http://superuser.com/questions/306497/can-linux-mount-a-normal-time-machine-sparse-bundle-disk-image-directory)
- [FUSE filesystem for reading Mac OS sparse-bundle disk images](https://github.com/torarnv/sparsebundlefs)

## Copy sparse bundle

If it's [block level incremental backup (BLIB)](https://en.wikipedia.org/wiki/Incremental_backup#Block_level_incremental) or if the [rsync algorithm](https://en.wikipedia.org/wiki/Rsync#Algorithm) is used for unencrypted sparse bundle, the band size is not important, smaller size you should be considered for the traffic impact

- [mac - Backup strategy for developer-focused Apple environments? - Server Fault](http://serverfault.com/questions/575357/backup-strategy-for-developer-focused-apple-environments)
- [backup - What is a safe way to back up a sparsebundle that is exported via afpd? - Server Fault](http://serverfault.com/questions/594939/what-is-a-safe-way-to-back-up-a-sparsebundle-that-is-exported-via-afpd)
- [hdiutil(1) Mac OS X Manual Page](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/hdiutil.1.html)