APNG used by iMessage stickers: [tinify/iMessage-Panda-sticker: Animated PNG example iMessage sticker for iOS 10, with waving panda!](https://github.com/tinify/iMessage-Panda-sticker)

Absolute coordinates can be store separatly (see [Metadata](#metadata)): [Image Offset (oFFs) - PNG Options and Extensions (PNG: The Definitive Guide)](http://www.libpng.org/pub/png/book/chapter11.html#png.ch11.div.10)

Text and annotation can be included (see [Metadata](#metadata)): [International Text Annotations (iTXt) - PNG Options and Extensions (PNG: The Definitive Guide)](http://www.libpng.org/pub/png/book/chapter11.html#png.ch11.div.4) and [Latin-1 Text Annotations (tEXt, zTXt) - PNG Options and Extensions (PNG: The Definitive Guide)](http://www.libpng.org/pub/png/book/chapter11.html#png.ch11.div.3)

For PNG to be 32 bits:

	mogrify -background none -define png:color-type=6 image.png

## Format

See also MNG

>  PNG doesn't technically use 32-bit unsigned integers; it uses 31-bit unsigned integers padded with an extra zero bit. This was done to accommodate languages which don't have unsigned integer types. The upper limit on image width or height is thus 2^31-1 or 2,147,483,647.
— [File format limits in pixel size for png images? - Stack Overflow](https://stackoverflow.com/questions/4109447/file-format-limits-in-pixel-size-for-png-images#comment6064319_4109505)

- [Portable Network Graphics (PNG) Specification (Second Edition)](https://www.w3.org/TR/PNG/)
- [How PNG Works – Medium](https://medium.com/@duhroach/how-png-works-f1174e3cc7b7#.hwnsb5d2l)
- [InspectPNG - Often PNG files contains hidden messages](http://opcoders.com/inspectpng)
- [TweakPNG](http://entropymine.com/jason/tweakpng/)
- [mikechambers/as3corelib: An ActionScript 3 Library that contains a number of classes and utilities for working with ActionScript? 3. These include classes for MD5 and SHA 1 hashing, Image encoders, and JSON serialization as well as general String, Number and Date APIs.](https://github.com/mikechambers/as3corelib)
- [ActionScript (AS3) library for processing binary data](https://github.com/blooddy/blooddy_crypto)
- https://github.com/HaxeFoundation/format/tree/master/format/png
- [Performance Calendar » PNG that works](http://calendar.perfplanet.com/2010/png-that-works/)
- [photopea/UPNG.js: Fast and advanced PNG decoder](https://github.com/photopea/UPNG.js)

## Fireworks PNG

Contains vector shapes. Use IDAT chunks + prVW, mkBF, mkTS, mkBS, mkBT chunks

- [image processing - The fireworks PNG format, any insight? Any libs? - Stack Overflow](https://stackoverflow.com/questions/4242402/the-fireworks-png-format-any-insight-any-libs)
- [XnView Software • View topic - iPhone Flavor of PNG format](http://newsgroup.xnview.com/viewtopic.php?f=35&t=20592#p86243)
- [Analysis of Fireworks PNG Support](http://www.vias.org/pngguide/chapter01_04_04.html)
- [Use Fireworks for PNGs? Ever look inside them? You need to. – No, I am better than that!](https://rickosborne.org/blog/2007/10/use-fireworks-for-pngs-ever-look-inside-them-you-need-to/)
- [Reading Fireworks PNG — Programmers Heaven](http://www.programmersheaven.com/discussion/366107/reading-fireworks-png)
- [Macromedia Fireworks - Exporting and saving files: The Fireworks file paradigm](http://web.archive.org/web/20160409193718/http://www.adobe.com/support/fireworks/export/fw_export_vs_sav/fw_export_vs_sav02.html)

## APNG

MNG is very similar to APNG

- [Inter-frame Optimization in APNG](http://littlesvr.ca/apng/inter-frame.html)
- [APNG Specification - MozillaWiki](https://wiki.mozilla.org/APNG_Specification)
- [APNG tests](https://philip.html5.org/tests/apng/tests.html)
- [APNG — Wikipedia](https://en.wikipedia.org/wiki/APNG)
- [APNG Assembler download | SourceForge.net](https://sourceforge.net/projects/apngasm/)
- [APNG Disassembler download | SourceForge.net](https://sourceforge.net/projects/apngdis/)
- [onevcat/APNGKit: High performance and delightful way to play with APNG format in iOS.](https://github.com/onevcat/APNGKit)
- [gif2apng.sf.net - Convert GIF to APNG](http://gif2apng.sourceforge.net/)
- [APNG - Browse /APNG_Optimizer at SourceForge.net](https://sourceforge.net/projects/apng/files/APNG_Optimizer/)
- [Test apng memory usage](http://people.igalia.com/clopez/apngmem/withapng.html)
- [Animated PNGs — Create APNGs, Animated PNG / APNG Maker](http://animatedpngs.com/) - see [Deckromancy/AnimatedEncoder: A Javascript Library that allows you export to Animated Formats such as Animated PNG and Animated WEBP, leaveraging the browser's native encoding support to optimize performance. It is also useful for non-animated PNG. It can create lossy-style PNGs with a JPEG-like 0.0 - 1.0 quality parameter. The PNG will be optimized, quantizing and dithering uncommon colors. It can maintain good quality while greatly reducing file size. Animated PNG will be supported in the majority of the 4 big browsers soon (Safari, Firefox, Chrome) when Chrome support is added, anticipated by the end of 2016. WEBP is making advancements as well, with more browsers testing it.](https://github.com/Deckromancy/AnimatedEncoder)
- [A (animated) PNG decoder in JavaScript for the HTML5 canvas element and Node.js](https://github.com/devongovett/png.js)
- `wget -q http://sourceforge.net/projects/apngasm/files/2.2/apngasm-2.2-bin-linux.zip/download -O apngasm-2.2-bin-linux.zip && unzip apngasm-2.2-bin-linux.zip && chmod +x apngasm` then `/apngasm frames.png frame000* 1 /l0`
- [257263 - (apngspec) APNG spec discussion](https://bugzilla.mozilla.org/show_bug.cgi?id=257263)
- [davidmz/apng-canvas: APNG implementation on canvas.](https://github.com/davidmz/apng-canvas)
- [rauchg/APNG: Animated PNG cross-browser utility.](https://github.com/rauchg/APNG)
- [shutej/apng](https://github.com/shutej/apng) - This is a fork of code in Go's image/png package for encoding APNG
- `ffmpeg -i in.mkv -vcodec apng -an out.png` (start v3.3 `d75984486399e655cbcba098e986ced4e1187efa`)
- [APNG Assembler](http://apngasm.sourceforge.net/)

## Compression

Compared to other formats:

- [GIF vs APNG vs WebP](http://littlesvr.ca/apng/gif_apng_webp.html)
- [FRDX - PNG vs WebP](http://frdx.free.fr/png_vs_webp.htm)

> *The Jared Wilcurt* compiled this list of image optimization resources. He has spent years crafting the following recipe for maximum png compression without loss of quality. He recommends the following:
> 
> 1. Use **TruePNG** first to convert to the [correct type of PNG](http://www.css-ig.net/png-test-corpus.html) format using:`TruePNG /o4 0.png /out 0.t.png`
> 2. Run your png(s) through **PngOptimizer**, it's pretty fast and does a good job. [My settings](http://imgur.com/eLXcMD3).
> 3. Then run it in **zopflipng** with it set to test all modes. This will by far take the longest amount of time. Settings: `zopflipng --iterations=1000 --splitting=3 --filters=01234mepb --lossy_transparent 0.png 0.zopfli.png`
> 4. Run them through **PNGOUTWin**, it does a good job of finding ways to compress PNGs other algorithms won't. [My settings](http://imgur.com/QG2qI5m).
> 5. Now Run them through **PNGGauntlet**. Since it's using DeflOpt, PNGGauntlet can't be ran before PngOptimizer or PNGOUTWin, or it will prevent them from doing the maximum compression they could otherwise do. [My Settings](http://imgur.com/jzjp4hD).
> 6. Finally running **defluff** after DeflOpt can scrape off a few bytes.
> 7. ... But also sometimes running **DeflOpt** after defluff can shave off a few bytes. Soooo run it again (via PNGGauntlet).

Tools and infos:

- [A Picture Costs A Thousand Words](http://www.slideshare.net/guypod/a-picture-costs-a-thousand-words18062013/12) - see [A picture costs a thousand words](a-20picture-20costs-20a-20thousand-20words-130619124428-phpapp01.pdf#page=12)
- [The smallest 256x256 single-color PNG file, and where you've seen it](https://www.mjt.me.uk/posts/smallest-png/)
- [PNG Test Corpus (2017)](http://css-ig.net/png-test-corpus)
- [PNGQuant](http://pngquant.org/)
- [Pngnq](http://pngnq.sourceforge.net/)
- [PNGCrush](http://pmt.sourceforge.net/pngcrush/)
- [OptiPNG](http://optipng.sourceforge.net/)
- [PNGOut](http://advsys.net/ken/utils.htm) (Win) and [pngwolf](http://bjoern.hoehrmann.de/pngwolf)
- [https://github.com/subzey/zopfli-png](zopfli-png) and [Pngnq S9](http://sourceforge.net/projects/pngnqs9/)
- [ScriptPNG](http://css-ig.net/scriptpng) (Win CMD) use AdvDef, DeflOpt, Defluff, Huffmix, PNGOut, PNGQuant, PNGWolf, PNGZopfli, TruePNG and Zopfli
- [PNG, JPG and GIF optimizers](http://css-ig.net/tools/)
- [PNG Compression : 5 simple improvements](http://mainroach.blogspot.fr/2013/09/png-compression-5-simple-improvements.html)
- [PNG Bloat in Android Games](http://mainroach.blogspot.fr/2014/03/png-bloat-in-android-games.html)
- [PNGGauntlet](http://pnggauntlet.com/) use PNGOut, OptiPNG, and DeflOpt
- [Huffmix](http://frdx.free.fr/huffmix/) use PNGOut with random modes (see also [the Thread about it on encode.ru](http://encode.ru/threads/1313-Huffmix-a-PNGOUT-r-catalyst))
- [PNGWolf](https://github.com/hoehrmann/pngwolf) (see also [the Thread about it on encode.ru](http://encode.ru/threads/1262-pngwolf))
- [TruePNG](http://x128.ho.ua/pngutils.html) (see also [TruePNG tutorial](http://css-ig.net/articles/truepng)) right ColorType chooser, palette optimizer (ordering) and clear full transparent RGB data
- [PNGKT](http://x128.ho.ua/pngutils.html) (older version of TruePNG)
- [Median Cut Posterizer](https://github.com/pornel/mediancut-posterizer)
- [CryoPNG](http://frdx.free.fr/cryopng/) (see also [the Thread about it on encode.ru](http://encode.ru/threads/1260-CryoPNG-short-introduction)) clear full transparent RGB data
- [PunyPNG](http://www.punypng.com/) (online tool) clear full transparent RGB data
- [PNG Optimizer](http://psydk.org/PngOptimizer) (Win)
- [PNG rewrite](http://entropymine.com/jason/pngrewrite/) (Win)
- [PNGnq-s9](http://sourceforge.net/projects/pngnqs9/) (modified version of Pngnq)
- [PNG Tools Overview](http://css-ig.net/png-tools-overview)
- [Comparison of lossless PNG compression tools](http://www.olegkikin.com/png_optimizers/)
- [PNGOut vs PNGWolf+zopfli](http://encode.ru/threads/1703-pngout-vs-pngwolf-zopfli) https://github.com/MrKrzYch00/zopfli
- [Test d'organisation de palette pour les PNG8](http://css-ig.net/articles/test-organisation-palette-png8)
- [pngthermal](http://frdx.free.fr/png.htm) use to view compression efficiency (similar too gzthermal) (see also [the Thread about it on encode.ru](http://encode.ru/threads/1725-pngthermal-pseudo-thermal-view-of-PNG-compression-efficiency))
- [Impact of palette order](http://css-ig.net/articles/outil-couleurs-palette)
- [Reduce PNG32 weight](http://css-ig.net/articles/diminuer-poids-png32)
- [PNG can be a lossy format](http://pngmini.com/lossypng.html)
- [Overview of PNG optimization tools](http://css-ig.net/png-tools-overview.html)
- [Comparison of png optimisation tools | ImageOptim-CLI](http://jamiemason.github.io/ImageOptim-CLI/comparison/png/photoshop/desc/)
- [pngquant vs pngcrush vs optipng vs pngnq - Archive - Pointless Ramblings](http://pointlessramblings.com/posts/pngquant_vs_pngcrush_vs_optipng_vs_pngnq/)
- [Zopfli Optimization: Literally Free Bandwidth](http://blog.codinghorror.com/zopfli-optimization-literally-free-bandwidth/)
- [Reducing PNG file Size — Medium](https://medium.com/@duhroach/reducing-png-file-size-8473480d0476)
- [pingo, a fast image optimizer](http://css-ig.net/pingo)
- [png and jpg size optimization scripts](https://github.com/clyfish/pngopt)
- [shssoichiro/oxipng: PNG optimizer written in Rust](https://github.com/shssoichiro/oxipng)

zlib-compatible (gzip, deflate):

- [Zopfli](https://github.com/google/zopfli) and [PNGZopfli (deficated tool for PNG)](https://github.com/google/zopfli/blob/master/README.zopflipng) (see also [the Thread about it on encode.ru](http://encode.ru/threads/1689-Google-Compress-Data-More-Densely-with-Zopfli) and [another one for ZopfliPNG](http://encode.ru/threads/1717-ZopfliPNG))
- [AdvDef / AdvanceCOMP (for PNG, MNG, GZ, TGZ and SVGZ)](http://advancemame.sourceforge.net/doc-advdef.html) and [AdvPNG (decidated tool for PNG)](http://advancemame.sourceforge.net/doc-advpng.html)
- [DeflOpt](http://www.walbeehm.com/download/) (Win, Unix?) support GZIP, PNG and ZIP files (see also [the Thread about it on encode.ru](http://encode.ru/threads/455-Ben-Jos-Walbeehm-s-DeflOpt-what-does-it-actually-do))
- [Defluff](http://encode.ru/tags.php?tag=defluff)
- [ScriptGZIP](http://css-ig.net/scriptgzip) (Win CMD)
- [gzthermal](http://frdx.free.fr/def.htm) use to view compression efficiency (see also [the Thread about it on encode.ru](http://encode.ru/threads/1889-gzthermal-pseudo-thermal-view-of-Gzip-Deflate-compression-efficiency))

## Deflate

See [Deflate](Deflate)

## Metadata

`-strip`
`-define png:include-chunk=none -set colorspace Gray`
`-define png:bkgd=no png:iccp=no`
`-define png:ancillary=no`
`-define png:include-chunk=gama`
`-define png:exclude-chunk=EXIF,cHRM,bKGD,iCCP,iTXt,sRGB,tEXt,zCCP,zTXt,tIME,date` (see also [`zopflipng`](https://github.com/google/zopfli))

bKGD
cHRM
gAMA
tIME
tEXt

`+set date:create +set date:modify`

Add tTXt:

	convert INFILE.png -set Title "foobar the great" OUTFILE.png
	identify -verbose OUTFILE.png

- `-comment` option [ImageMagick: Command-line Options](http://www.imagemagick.org/script/command-line-options.php#comment)
- `-define` option [ImageMagick: Command-line Options](http://www.imagemagick.org/script/command-line-options.php#define)
- https://github.com/ImageMagick/png/blob/master/png.h

## Apple specific

Apple's proprietary CgBI format.

- https://github.com/DHowett/pincrush
- http://iphonedevwiki.net/index.php/CgBI_file_format

Decode:

	# From https://gist.github.com/urielka/3609051/28debdadc4e4b17e1ccec779241999fd974051f5
	#---
	# iPIN - iPhone PNG Images Normalizer v1.0
	# Copyright (C) 2007
	#
	# Author:
	#  Axel E. Brzostowski
	#  http://www.axelbrz.com.ar/
	#  axelbrz@gmail.com
	# 
	# References:
	#  http://iphone.fiveforty.net/wiki/index.php/PNG_Images
	#  http://www.libpng.org/pub/png/spec/1.2/PNG-Contents.html
	# 
	# This program is free software: you can redistribute it and/or modify
	# it under the terms of the GNU General Public License as published by
	# the Free Software Foundation, either version 3 of the License.
	# 
	# This program is distributed in the hope that it will be useful,
	# but WITHOUT ANY WARRANTY; without even the implied warranty of
	# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
	# GNU General Public License for more details.
	# 
	#---
	
	from struct import *
	from zlib import *
	import stat
	import sys
	import os
	
	def getNormalizedPNG(filename):
		pngheader = "\x89PNG\r\n\x1a\n"
	
		file = open(filename, "rb")
		oldPNG = file.read()
		file.close()
	
		if oldPNG[:8] != pngheader:
			return None
	
		newPNG = oldPNG[:8]
	
		chunkPos = len(newPNG)
	
		idatAcc = ""
		breakLoop = False
	
		# For each chunk in the PNG file	
		while chunkPos < len(oldPNG):
			skip = False
		
			# Reading chunk
			chunkLength = oldPNG[chunkPos:chunkPos+4]
			chunkLength = unpack(">L", chunkLength)[0]
			chunkType = oldPNG[chunkPos+4 : chunkPos+8]
			chunkData = oldPNG[chunkPos+8:chunkPos+8+chunkLength]
			chunkCRC = oldPNG[chunkPos+chunkLength+8:chunkPos+chunkLength+12]
			chunkCRC = unpack(">L", chunkCRC)[0]
			chunkPos += chunkLength + 12
	
			# Parsing the header chunk
			if chunkType == "IHDR":
				width = unpack(">L", chunkData[0:4])[0]
				height = unpack(">L", chunkData[4:8])[0]
	
			# Parsing the image chunk
			if chunkType == "IDAT":
				# Store the chunk data for later decompression
				idatAcc += chunkData
				skip = True
	
			# Removing CgBI chunk		
			if chunkType == "CgBI":
				skip = True
	
			# Add all accumulated IDATA chunks
			if chunkType == "IEND":
				try:
					# Uncompressing the image chunk
					bufSize = width * height * 4 + height
					chunkData = decompress( idatAcc, -15, bufSize)
				
				except Exception, e:
					# The PNG image is normalized
					print e
					return None
	
				chunkType = "IDAT"
	
				# Swapping red & blue bytes for each pixel
				newdata = ""
				for y in xrange(height):
					i = len(newdata)
					newdata += chunkData[i]
					for x in xrange(width):
						i = len(newdata)
						newdata += chunkData[i+2]
						newdata += chunkData[i+1]
						newdata += chunkData[i+0]
						newdata += chunkData[i+3]
	
				# Compressing the image chunk
				chunkData = newdata
				chunkData = compress( chunkData )
				chunkLength = len( chunkData )
				chunkCRC = crc32(chunkType)
				chunkCRC = crc32(chunkData, chunkCRC)
				chunkCRC = (chunkCRC + 0x100000000) % 0x100000000
				breakLoop = True
	
			if not skip:
				newPNG += pack(">L", chunkLength)
				newPNG += chunkType
				if chunkLength > 0:
					newPNG += chunkData
				newPNG += pack(">L", chunkCRC)
			if breakLoop:
				break
		
		return newPNG
	
	def updatePNG(filename):
		data = getNormalizedPNG(filename)
		if data != None:
			file = open(filename, "wb")
			file.write(data)
			file.close()
			return True
		return data
	
	def getFiles(base):
		global _dirs
		global _pngs
		if base == ".":
			_dirs = []
			_pngs = []
		
		if base in _dirs:
			return
	
		files = os.listdir(base)
		for file in files:
			filepath = os.path.join(base, file)
			try:
				st = os.lstat(filepath)
			except os.error:
				continue
		
			if stat.S_ISDIR(st.st_mode):
				if not filepath in _dirs:
					getFiles(filepath)
					_dirs.append( filepath )
				
			elif file[-4:].lower() == ".png":
				if not filepath in _pngs:
					_pngs.append( filepath )
			
		if base == ".":
			return _dirs, _pngs
	
	print "-----------------------------------"
	print " iPhone PNG Images Normalizer v1.0"
	print "-----------------------------------"
	print " "
	print "[+] Searching PNG files...",
	dirs, pngs = getFiles(".")
	print "ok"
	
	if len(pngs) == 0:
		print " "
		print "[!] Alert: There are no PNG files found. Move this python file to the folder that contains the PNG files to normalize."
		exit()
	
	print " "
	print " -  %d PNG files were found at this folder (and subfolders)." % len(pngs)
	print " "
	while True:
		normalize = raw_input("[?] Do you want to normalize all images (Y/N)? ").lower()
		if len(normalize) > 0 and (normalize[0] == "y" or normalize[0] == "n"):
			break
	
	normalized = 0
	if normalize[0] == "y":
		for ipng in xrange(len(pngs)):
			perc = (float(ipng) / len(pngs)) * 100.0
			print "%.2f%% %s" % (perc, pngs[ipng])
			if updatePNG(pngs[ipng]):
				normalized += 1
	print " "
	print "[+] %d PNG files were normalized." % normalized

## Decompression Bomb

- [Decompression Bomb](Deflate#Decompression Bomb)

A very big image with could take 18.44 TB (2147483647x2147483647x4) of memory for uncompressed data 13.83TB