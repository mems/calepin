It's impossible to know the uncompressed size without read all data.

gzip is file format used to compress. It use [deflate](../Deflate/Deflate.md) compression algorithm

gzip is GZIP headers, DEFLATE data (compressed data), and a checksum

zlib is the most common library to handle gzip file format

Compress gzip without save filename and timestamp `gzip -9 -n -k -f file`

- [Zopfli](http://code.google.com/p/zopfli/) (see also [the Thread about it on encode.su](https://encode.su/threads/1689-Google-Compress-Data-More-Densely-with-Zopfli))
- [DeflOpt](http://www.walbeehm.com/download/) (Win, Unix?) support GZIP, PNG and ZIP files (see also [the Thread about it on encode.su](https://encode.su/threads/455-Ben-Jos-Walbeehm-s-DeflOpt-what-does-it-actually-do))
- [Defluff](https://encode.su/tags.php?tag=defluff)
- [ScriptGZIP](http://css-ig.net/scriptgzip) (Win CMD)
- [gzthermal](http://frdx.free.fr/def.htm) use to view compression efficiency (see also [the Thread about it on encode.su](https://encode.su/threads/1889-gzthermal-pseudo-thermal-view-of-Gzip-Deflate-compression-efficiency))

- [zlib Technical Details](http://www.zlib.net/zlib_tech.html)

## Resources

- [Gzip - ForensicsWiki](http://www.forensicswiki.org/wiki/Gzip)
- [gzthermal: pseudo thermal view of Gzip/Deflate compression efficiency](https://encode.su/threads/1889-gzthermal-pseudo-thermal-view-of-Gzip-Deflate-compression-efficiency)
- [Huffmix: a PNGOUT -r catalyst](https://encode.su/threads/1313-Huffmix-a-PNGOUT-r-catalyst)
- [defdb a tool to dump the deflate stream from .gz and .png files](https://encode.su/threads/1428-defdb-a-tool-to-dump-the-deflate-stream-from-gz-and-png-files)
- [SharpZipLib/src/ICSharpCode.SharpZipLib/GZip at master · icsharpcode/SharpZipLib](https://github.com/icsharpcode/SharpZipLib/tree/master/src/ICSharpCode.SharpZipLib/GZip)

## Concatenation

You can concatenate/merge multiple gzip in one gzip:

	echo 1 > 1.txt ; echo 2 > 2.txt; echo 3 > 3.txt;
	gzip 1; gzip 2; gzip 3;
	cat 1.gz 2.gz 3.gz > all.gz

	gunzip -c all.gz > all.txt

	cat all.txt
	# will output:
	1
	2
	3

The same as `cat 1.txt 2.txt 3.txt`

Can be usefull when you want add a small data before or after a big chunk already compressed

- [GNU Gzip](https://www.gnu.org/software/gzip/manual/gzip.html#Advanced-usage)
- https://tools.ietf.org/html/rfc1952#page-5
- [Is there a GZIP merger that merges two GZIP files without decompressing them? - Stack Overflow](https://stackoverflow.com/questions/274185/is-there-a-gzip-merger-that-merges-two-gzip-files-without-decompressing-them)
