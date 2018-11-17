- [Mojibake — Wikipedia](https://en.wikipedia.org/wiki/Mojibake) - "is the garbled text that is the result of text being decoded using an unintended character encoding"

- [Byte order mark — Wikipedia](https://en.wikipedia.org/wiki/Byte_order_mark)
- [UTF-8 and Unicode Standards](http://www.utf-8.com/)
- [UTF-8 Everywhere](http://utf8everywhere.org/)
- [RFC 3629 - UTF-8, a transformation format of ISO 10646](https://tools.ietf.org/html/rfc3629)
- [Unicode Consortium](http://www.unicode.org/)
- [Unicode Codepoint Chart](http://inamidst.com/stuff/unidata/) and http://inamidst.com/stuff/unidata/unidata.sh
- [A Programmer’s Introduction to Unicode – Nathan Reed’s coding blog](http://reedbeta.com/blog/programmers-intro-to-unicode/)
- [Mechanism and Its Consequences : Validating UTF8 strings with Lookup Tables](http://darkcephas.blogspot.com/2018/10/validating-utf8-strings-with-lookup.html) - [darkcephas/utf8Validity_lookupTable: Non SIMD optimized utf8 string validator](https://github.com/darkcephas/utf8Validity_lookupTable)

UTF-8 est suffisamment intelligent pour coder les chars < 128 sur 1 byte et donc seulement les chars > 128 sur 2 bytes

ANSI ( les ASCII < 128 ,plus les codepages > 128 jusqu'a 255)
Unicode ( UTF-16/UCS-2, little endian , cad 2 bytes sont utilisés pour chaque char)
Unicode Big Endian ( UTF-16/UCS-2, big endian, idem 2 bytes par char )
UTF-8 ( 1 byte par char < 128, 2 bytes par char > 128) 

- [What Every Programmer Absolutely, Positively Needs to Know About Encodings and Character Sets to Work With Text](http://kunststube.net/encoding/)
- [UTF-8 — Wikipedia](https://en.wikipedia.org/wiki/UTF-8)
- [Unicode — Wikipedia](https://en.wikipedia.org/wiki/Unicode#UTF)
- Why the `FAMILY` emoji has a `.length` of 8 (2 for each emoji and 1 for each zero-width joiner) [Emoji.prototype.length — a tale of characters in Unicode - Contentful](https://www.contentful.com/blog/2016/12/06/unicode-javascript-and-the-emoji-family/)

- https://github.com/mathiasbynens/utf8.js
 
	function encodeUTF8(string) {
		var utftext = "";
	
		for (var n = 0; n < string.length; n++) {
		
			var c = string.charCodeAt(n);
		
			if (c < 128) {
				utftext += String.fromCharCode(c);
			}
			else if((c > 127) && (c < 2048)) {
				utftext += String.fromCharCode((c >> 6) | 192);
				utftext += String.fromCharCode((c & 63) | 128);
			}
			else {
				utftext += String.fromCharCode((c >> 12) | 224);
				utftext += String.fromCharCode(((c >> 6) & 63) | 128);
				utftext += String.fromCharCode((c & 63) | 128);
			}
		
		}
	
		return utftext;
	}

## Continuation bytes

Can be used to count code points (unicode chars): skip all bytes start with 10xxxxxx

	// Count UTF-8 chars:
	while (*c) count += ((*(c++) & 0xC0) == 0x80) ? 0 : 1;

Are part of non first bytes of multi bytes char.

- [unicode - UTF-8 Continuation bytes - Stack Overflow](https://stackoverflow.com/questions/9356169/utf-8-continuation-bytes/9356203#9356203)