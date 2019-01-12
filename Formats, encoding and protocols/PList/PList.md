- [Property list - Wikipedia](https://en.wikipedia.org/wiki/Property_list)

Start with `bplist00` (binary plists)

## typedstream data

Similar (and old) format: `<0x04><0x0b>streamtyped`

- `typedstream.h`
	> You can use typedstreams to save arbitrary C data, including Objective C objects, onto an arbitrary stream (see NXStream)
	> [...]
	> Not only data structures are written, but also their type, allowing for retrieval even in the absence of the code used for saving them
- `NSCompatibility.h`
- [objective c - Is there a way to read in files in TypedStream format - Stack Overflow](https://stackoverflow.com/questions/4371588/is-there-a-way-to-read-in-files-in-typedstream-format)
- [Legacy File Formats](http://www.stone.com/The_Cocoa_Files/Legacy_File_Formats.html)
- [Apple - Lists.apple.com](https://lists.apple.com/archives/Cocoa-dev/2005/Jan/msg00736.html) - NSUnarchiver and StickiesDatabase
- http://www.opensource.apple.com/source/CF/CF-744.19/CFBinaryPList.c

## Convertion

	# Rewrite the source file with given format
	plutil -convert xml1 data.plist

	# Output to desired format (json, xml1 or binary1)
	# Not date and data fields can't be converted to JSON (error "invalid object in plist for destination format")
	plutil -convert json -o - file.plist
	plutil -convert xml1 -o - - < data.plist
	# fix plist to JSON using only commands available on macOS
	plutil -convert json -o - file.plist | php -r "echo json_encode(simplexml_load_file('php://stdin','SimpleXMLElement',LIBXML_NOCDATA));"

- [`plutil` が json 形式にコンバートしてくれないっ、てゆのは - ばかもりだし](http://baqamore.hatenablog.com/entry/2017/01/28/051955)
- [PlistEdit Pro Help](https://fatcatsoftware.com/plisteditpro/Docs/print/index.html#about-json) - About JSON and data types of PList

## Tools and libraries

- libplist
- [plutil(1) Mac OS X Manual Page](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/plutil.1.html)
- [Converting Binary Plists - ForensicsWiki](http://www.forensicswiki.org/wiki/Converting_Binary_Plists)
- [3breadt/dd-plist: A java library providing support for ASCII, XML and binary property lists.](https://github.com/3breadt/dd-plist)
- [ladinu/bplist: Binary plist parser and creator for node.js](https://github.com/ladinu/bplist) - Use [joeferner/node-bplist-parser: Binary plist parser.](https://github.com/joeferner/node-bplist-parser) and [joeferner/node-bplist-creator: Binary Mac OS X Plist (property list) creator.](https://github.com/joeferner/node-bplist-creator)
- [ckruse/CFPropertyList: Read, write and manipulate both binary and XML property lists as defined by apple](https://github.com/ckruse/CFPropertyList)
- [wollardj/node-simple-plist: A simple API for interacting with binary and plain text plist data.](https://github.com/wollardj/node-simple-plist)
- [CFBinaryPList.c](http://opensource.apple.com/source/CF/CF-550/CFBinaryPList.c)
- [dpearson/plist.js: Javascript library for reading and creating Apple Property Lists (XML and ASCII only for now)](https://github.com/dpearson/plist.js) (handle ASCII, XML plist)
- [initial binary plist implementation in nodejs](https://gist.github.com/clee/1007217#file-binary-plist-js)
- [objective c - Command-line tool for converting PLIST to JSON? - Stack Overflow](https://stackoverflow.com/questions/6066350/command-line-tool-for-converting-plist-to-json)
- [Reverse Engineering Instruments’ File Format](http://jamie-wong.com/post/reverse-engineering-instruments-file-format/#making-a-binary-plist-parser)
- [Marketcircle/bpylist: Parse and Generate binary plists and NSKeyedArchiver archives](https://github.com/Marketcircle/bpylist)
- [jorik041/ccl-bplist at 423670d84c118f66c9fe79122ba37dd856d23595](https://github.com/jorik041/ccl-bplist/tree/423670d84c118f66c9fe79122ba37dd856d23595)

JavaScript implementation:

> From what I understand, all Javascript implementations store numbers internally as doubles (even what appear to be integers!)[1]. There are two problems; the first one is that bplists can contain 32-bit floats as well as 64-bit doubles, and so you need two separate code paths for decoding them into the native JS Number type. The other problem is that decoding them is not exactly straightforward - there's no simple way I've found yet to unpack a 4-byte buffer into a float, or an 8-byte buffer into a double.
> 
> The good news is, solving the double case also solves the date case - all dates in bplists are stored as a 64-bit double value, which is an offset since the epoch (although I think Apple uses a different epoch than the usual UNIX one). Anyway, once we can parse doubles correctly, dates should be trivial to implement.
— https://github.com/TooTallNate/plist.js/issues/2#issuecomment-1299675

> as @clee mention above, Apple isn't using UNIX epoch for dates, rather using it's own epoch which is relative to Jan 1 2001 00:00:00 GMT in seconds. Check CoreFoundation's CFDateGetAbsoluteTime(theDate) for more information.
> 
> 	function toDate(absoluteTime){
> 	    var time = 978307200000;  // relation to unix epoc in millisecounds (should be correct).
> 	    time = time  + (absoluteTime * 1000);
> 	    return new Date(time);
> 	}
— https://github.com/TooTallNate/plist.js/issues/2#issuecomment-7286244

> Wondering what you consider a viable strategy for detecting binary plists? I was thinking something along these lines:
> 
> 	// detect if a file is ascii by looking for an octet with a val > 127
> 	// @param plist the content of the plist file as a string
> 	function fileIsAscii(plist) {
> 	    // as soon as we hit an octet > 127, we prob have binary
> 	    for (var i=0, len=plist.length; i<len; i++) {
> 	      if (plist[i] > 127) { return false; }
> 	    }
> 	    return true;
> 	}
— https://github.com/TooTallNate/plist.js/issues/2#issuecomment-8882075


	function toDate(str){
		// new Date(str) ??
		let dt = str.split("T");
		let ymd = dt[0].split("-");
		let hms = dt[1].split("Z")[0].split(":");
		let date = new Date();
		date.setUTCFullYear(ymd[0]);
		date.setUTCMonth(ymd[1] - 1);
		date.setUTCDate(ymd[2]);
		date.setUTCHours(hms[0]);
		date.setUTCMinutes(hms[1]);
		date.setUTCSeconds(hms[2]);
		return date;
	}
