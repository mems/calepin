Display as human readable where `X` from `<CFKeyedArchiverUID ...>{value = X}` is the index in `$objects` array

	plutil -p data.plist

- `NSKeyedUnarchiver.unarchiveObjectWithData()`
- [Geek post: NSKeyedArchiver files – what are they, and how can I use them? | Digital Investigation](https://digitalinvestigation.wordpress.com/2012/04/04/geek-post-nskeyedarchiver-files-what-are-they-and-how-can-i-use-them/)
- [cclgroupltd/ccl-bplist: Python Module for parsing Binary Property List and NSKeyedArchiver files](https://github.com/cclgroupltd/ccl-bplist)
- [Manual Analysis of ‘NSKeyedArchiver’ Formatted Plist Files - A Review of the NEW OS X 10.11 “Recent Items” — mac4n6.com](https://www.mac4n6.com/blog/2016/1/1/manual-analysis-of-nskeyedarchiver-formatted-plist-files-a-review-of-the-new-os-x-1011-recent-items)
- [Reverse Engineering Instruments’ File Format](http://jamie-wong.com/post/reverse-engineering-instruments-file-format/#making-a-binary-plist-parser)
	- [speedscope/instruments.ts at 9edd5ce7ed6aaf9290d57e85f125c648a3b66d1f · jlfwong/speedscope](https://github.com/jlfwong/speedscope/blob/9edd5ce7ed6aaf9290d57e85f125c648a3b66d1f/import/instruments.ts#L772) - `BinaryPlistParser`
	- [speedscope/instruments.ts at 9edd5ce7ed6aaf9290d57e85f125c648a3b66d1f · jlfwong/speedscope](https://github.com/jlfwong/speedscope/blob/9edd5ce7ed6aaf9290d57e85f125c648a3b66d1f/import/instruments.ts#L648) - `paternMatchObjectiveC`
- [Marketcircle/bpylist: Parse and Generate binary plists and NSKeyedArchiver archives](https://github.com/Marketcircle/bpylist)
- [ccl-bplist/ccl_bplist.py at 423670d84c118f66c9fe79122ba37dd856d23595 · jorik041/ccl-bplist](https://github.com/jorik041/ccl-bplist/blob/423670d84c118f66c9fe79122ba37dd856d23595/ccl_bplist.py#L354)
- [sketch-node-parser/msUnarchiver.js at 2fc464ec4bcead3cd04182021ef0c65c70557f93 · afiedler/sketch-node-parser](https://github.com/afiedler/sketch-node-parser/blob/2fc464ec4bcead3cd04182021ef0c65c70557f93/src/msArchiver/msUnarchiver.js#L16)