Optimize tarball by sorting by file extension and dir. `find ./source \! -type d | rev | sort | rev | tar cjf archive.tar.bz2 --files-from=-`
That group similar files together, allow compression from redundancy across files similar files.

You can ship with a manifest file (contains all file names) if the archive will contains lot of (heavy) files.

	find . > MANIFEST

- [Indexing large tar files for fast access using python | fomori blog](http://fomori.org/blog/?p=391)
- [devsnd/tarindexer: python module for indexing tar files for fast access](https://github.com/devsnd/tarindexer)
- [star(1): unique standard tape archiver - Linux man page](http://linux.die.net/man/1/star)

- [tar (computing) - Wikipedia](https://en.wikipedia.org/wiki/Tar_%28computing%29)
- http://www.cs.usfca.edu/~benson/cs326/pintos/pintos/src/lib/ustar.c
- [tar(5)](https://manpages.ubuntu.com/manpages/precise/en/man5/tar.5.html)

- [linux - List contents of large tar archive quickly - Super User](http://superuser.com/questions/712095/list-contents-of-large-tar-archive-quickly/712133#712133)

- [saibotsivad/signed-tar-manifest: Simple manifest generator to act as authoritative implementation of specs.](https://github.com/saibotsivad/signed-tar-manifest) and [saibotsivad/signed-tar: Specifications for a method of generating signed tar packages.](https://github.com/saibotsivad/signed-tar)

- [GNU tar blocking factor, blocks, records and checkpoints](https://finch.am/projects/tar/) - additional informations

## Tarbomb

- [tar (computing) — Wikipedia](https://en.wikipedia.org/wiki/Tar_%28computing%29#Tarbomb)
