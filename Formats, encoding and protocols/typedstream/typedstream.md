Similar to plist format

Magic header: `<0x04><0x0b>streamtyped`

- [depth42/MEUnarchiver: Attempt at implementing a replacement for NSUnarchiver which is not available under iOS. This can be handy for reading legacy file-formats on iOS devices. It does not provide all features of NSUnarchiver but the basic stuff is there.](https://github.com/depth42/MEUnarchiver)
- [cocotron/NSUnarchiver.m at master · berkus/cocotron](https://github.com/berkus/cocotron/blob/master/Foundation/NSUnarchiver.m)
- [libobjc/archive.c at master · gnustep/libobjc](https://github.com/gnustep/libobjc/blob/master/archive.c)
- [class-dump - Steve Nygard](http://stevenygard.com/projects/class-dump/)
- `typedstream.h`
	> You can use typedstreams to save arbitrary C data, including Objective C objects, onto an arbitrary stream (see NXStream)
	> [...]
	> Not only data structures are written, but also their type, allowing for retrieval even in the absence of the code used for saving them
- `NSCompatibility.h`
- [ios - Inspecting files of type "NeXT/Apple typedstream" version 4 (NSArchiver) - Stack Overflow](https://stackoverflow.com/questions/18834352/inspecting-files-of-type-next-apple-typedstream-version-4-nsarchiver/19167701#19167701)
- [objective c - Is there a way to read in files in TypedStream format - Stack Overflow](https://stackoverflow.com/questions/4371588/is-there-a-way-to-read-in-files-in-typedstream-format)
- [macos - Has anyone dig into the data format of the mac sticky notes database? - Stack Overflow](https://stackoverflow.com/questions/9951168/has-anyone-dig-into-the-data-format-of-the-mac-sticky-notes-database)
- [Legacy File Formats](http://www.stone.com/The_Cocoa_Files/Legacy_File_Formats.html)
- [Apple - Lists.apple.com](https://lists.apple.com/archives/Cocoa-dev/2005/Jan/msg00736.html) - NSUnarchiver and StickiesDatabase
- http://www.opensource.apple.com/source/CF/CF-744.19/CFBinaryPList.c
- [AAPL-Darwin - Browse /Darwin-0.1 at SourceForge.net](https://sourceforge.net/projects/aapl-darwin/files/Darwin-0.1/) - Darwin 0.3 re-built to run on x86 objc-1.tar.gz