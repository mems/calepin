It's compression algorithm

window size (32K sliding window): 32KB bytes

Ther is no official extension, but `.z` (or `.zz`) is usually used. See [List of archive formats — Wikipedia](https://en.wikipedia.org/wiki/List_of_archive_formats) and [java - Is there an official (or common) file extention or suffix for deflated files? - Stack Overflow](https://stackoverflow.com/questions/9806175/is-there-an-official-or-common-file-extention-or-suffix-for-deflated-files)

## zlib header

Valid zlib header must be divisible by 31

Examples:

- `78 01` - No Compression/low
- `78 9C` - Default Compression
- `78 DA` - Best Compression 

- [structure - What does a zlib header look like? - Stack Overflow](https://stackoverflow.com/questions/9050260/what-does-a-zlib-header-look-like)

## Resources

- `printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" | cat - zlib.bin | gzip -dc` zlib inflate
	- [compression - How to uncompress zlib data in UNIX? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/22834/how-to-uncompress-zlib-data-in-unix)
- `printf "\x1f\x8b\x08\x00\x00\x00\x00\x00\x00\x00" | cat - zlib-raw.bin | gzip -dc` zlib raw inflate
- `openssl zlib -d < zlib.bin`
- [DEFLATE — Wikipedia](https://en.wikipedia.org/wiki/DEFLATE)
- [defluff - a deflate huffman optimizer](https://encode.su/threads/1214-defluff-a-deflate-huffman-optimizer)
- [Simple compliant DEFLATE decompressor in Java](https://github.com/nayuki/Simple-DEFLATE-decompressor) and [Simple DEFLATE decompressor](https://www.nayuki.io/page/simple-deflate-decompressor)
- [Binary Formats in JavaScript: Base64, Deflate, and UTF8 - CodeProject](https://www.codeproject.com/Articles/26980/Binary-Formats-in-JavaScript-Base-Deflate-and-UT)
- https://github.com/dankogai/js-deflate and https://github.com/beatgammit/deflate-js
- https://github.com/imaya/zlib.js
- [nodeca/pako: high speed zlib port to javascript, works in browser & node.js](https://github.com/nodeca/pako)
- https://github.com/chrisdickinson/inflate
- https://github.com/oyvindln/deflate-rs
- https://github.com/PistonDevelopers/inflate
- https://github.com/mozilla/pdf.js FlateStream
- [Dissecting the GZIP format](http://commandlinefanatic.com/cgi-bin/showarticle.cgi?article=art001)
- [madler/infgen: Deflate disassember to convert a deflate, zlib, or gzip stream into a readable form.](https://github.com/madler/infgen) - `gcc infgen.c -o infgen && ./infgen -h`
- [java - How to find a good/optimal dictionary for zlib 'setDictionary' when processing a given set of data? - Stack Overflow](https://stackoverflow.com/questions/2011653/how-to-find-a-good-optimal-dictionary-for-zlib-setdictionary-when-processing-a)

## Decompression Bomb

- [Biggest image in the smallest space](https://www.bamsoftware.com/hacks/deflate.html)
- [LIBPNG](http://libpng.sourceforge.net/decompression_bombs.html)
- [Decompression bomb protection · Issue #515 · python-pillow/Pillow](https://github.com/python-pillow/Pillow/issues/515)
