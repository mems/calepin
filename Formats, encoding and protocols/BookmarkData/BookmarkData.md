BookmarkData is data structure used in OSX to keep reference to a file even in cases where the file was moved (on the same drive) or renamed

It's similar to finder Alias, but without magic header

Sometimes contained in [PList](./PList/PList.md) use the extension `.sfl`, ex: `~/Library/Application Support/com.apple.sharedfilelist/com.apple.LSSharedFileList.FavoriteServers.sfl`

- [Accessing Files and Directories](https://developer.apple.com/library/ios/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/AccessingFilesandDirectories/AccessingFilesandDirectories.html#//apple_ref/doc/uid/TP40010672-CH3-SW10)
- `URLByResolvingBookmarkData`
- [Apple's BookmarkData - exposed! – mikeymikey blogs here](http://michaellynn.github.io/2015/10/24/apples-bookmarkdata-exposed/)
- [al45tair / mac_alias — Bitbucket](https://bitbucket.org/al45tair/mac_alias) - `mac_alias` lets you generate or read binary Alias and Bookmark records from Python code.
- [\[.macos\] Add Finder sidebar (com.apple.sidebarlists) user defaults · Issue #693 · mathiasbynens/dotfiles](https://github.com/mathiasbynens/dotfiles/issues/693#issuecomment-238050609)
- [Working with SharedFileList (.sfl) files from OSX 10.11 El Capitan in python](https://gist.github.com/pudquick/4776b4b2075bf9b7e512)

Finder Alias is similar

Lookslike Sierra use an other format: [File system funnies in Sierra: folders that aren’t, and altered aliases – The Eclectic Light Company](https://eclecticlight.co/2016/12/06/file-system-funnies-in-sierra-folders-that-arent-and-altered-aliases/)

- [Alias (Mac OS) — Wikipedia](https://en.wikipedia.org/wiki/Alias_%28Mac_OS%29)
- [Some information about MacOS aliases collected from the web.](http://sebastien.kirche.free.fr/python_stuff/MacOS-aliases.txt)
- [osx - Why are the alias so big in filesize in Mountain Lion? - Ask Different](http://apple.stackexchange.com/questions/81671/why-are-the-alias-so-big-in-filesize-in-mountain-lion)
- [diimdeep/afsctool: AFSC (Apple File System Compression) tool](https://github.com/diimdeep/afsctool)
- [jrk/afsctool: Command line utility for analyzing and managing HFS+ compression.](https://github.com/jrk/afsctool)
- [Alias Manager - Core Services | Apple Developer Documentation](https://developer.apple.com/reference/coreservices/alias_manager)
- `osascript -e 'tell application "Finder" to make alias file to POSIX file "/file/to/make/link/from" at POSIX file "/folder/where/to/make/link"'`
- [SourceForge.net Repository - \[osxutils\] Contents of /osxutils/src/mkalias.c](http://osxutils.cvs.sourceforge.net/viewvc/osxutils/osxutils/src/mkalias.c?view=markup)
- [osx - How to use Mac Finder to list all aliases in a folder - Stack Overflow](https://stackoverflow.com/questions/21150169/how-to-use-mac-finder-to-list-all-aliases-in-a-folder/21151368#21151368)
- [objective c - How do I create a Finder alias within an application? - Stack Overflow](https://stackoverflow.com/questions/1928139/how-do-i-create-a-finder-alias-within-an-application)
- [A script to convert aliases to symlinks - Mac OS X Hints](http://hints.macworld.com/article.php?story=20021024064107356)
- [FSMegaInfo](https://developer.apple.com/library/content/samplecode/FSMegaInfo/Introduction/Intro.html)
- [CFAliasData v BookmarkData](http://www.magnusviri.com/Mac/cfaliasdata-vs-bookmarkdata.html)
- [Resolving Modern Mac Alia File | Indie Stack](https://indiestack.com/2017/05/resolving-modern-mac-alias-files/)
