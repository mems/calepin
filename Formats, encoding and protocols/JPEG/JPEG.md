Convert all PNG to JPEG with quality 90: `mogrify -verbose -format jpg -quality 90 *.png`

Lightroom infos:
> “0 quality” is not zero \[...\] “0-100” is really “0-12” \[eg. 13 grades\]
[Jeffrey Friedl's Blog » An Analysis of Lightroom JPEG Export Quality Settings](http://regex.info/blog/lightroom-goodies/jpeg-quality#surprise)

## Format

- [JPEG — Wikipedia](https://en.wikipedia.org/wiki/JPEG)
- [How JPG Works — Free Code Camp](https://medium.com/@duhroach/how-jpg-works-a4dbd2316f35)
- [mikechambers/as3corelib: An ActionScript 3 Library that contains a number of classes and utilities for working with ActionScript? 3. These include classes for MD5 and SHA 1 hashing, Image encoders, and JSON serialization as well as general String, Number and Date APIs.](https://github.com/mikechambers/as3corelib)
- [ActionScript (AS3) library for processing binary data](https://github.com/blooddy/blooddy_crypto)
- [JPEG 101 - How does JPEG work? - Arjun Sreedharan](http://arjunsreedharan.org/post/146070390717/jpeg-101-how-does-jpeg-work)
- [Getting JPG dimensions with AS3 without loading the entire file – Antti Kupila](http://www.anttikupila.com/flash/getting-jpg-dimensions-with-as3-without-loading-the-entire-file/)
- [Using Hardware to Decode and Load JPG Images up to 45% faster in Internet Explorer 11 – IEBlog](https://blogs.msdn.microsoft.com/ie/2013/09/12/using-hardware-to-decode-and-load-jpg-images-up-to-45-faster-in-internet-explorer-11/)
- [Jpeg Compression method](http://www.robertstocker.co.uk/jpeg/jpeg_new_7.htm)
- [Luma Chroma both - Chrominance — Wikipedia](https://en.wikipedia.org/wiki/Chrominance#mediaviewer/File:Luma_Chroma_both.png)
- [JPEG for the horseshoe crabs - JPEG_for_the_horseshoe_crabs.pdf](http://frdx.free.fr/JPEG_for_the_horseshoe_crabs.pdf)
- [PDF Reader in JavaScript](https://github.com/mozilla/pdf.js) - read JPEG and JPEG 2000
- [JPEG/DCT data decoder](https://github.com/notmasteryet/jpgjs) - read JPEG. share the same code from PDF.js
- https://github.com/HaxeFoundation/format/tree/master/format/jpg - write
- [JPEG for the horseshoe crabs - JPEG_for_the_horseshoe_crabs.pdf](http://wayback.archive.org/web/20160510122740/http://frdx.free.fr/JPEG_for_the_horseshoe_crabs.pdf)
- [Source Coding and Compression](http://iphome.hhi.de/schwarz/assets/pdfs/08_ImageCoding.pdf)
- [image processing - JPEG DCT padding - Signal Processing Stack Exchange](http://dsp.stackexchange.com/questions/35339/jpeg-dct-padding/35343)
- [ImpulseAdventure - JPEG Chroma Subsampling](http://www.impulseadventure.com/photo/chroma-subsampling.html)
- [The Metadata in JPEG files - Exiv2](http://dev.exiv2.org/projects/exiv2/wiki/The_Metadata_in_JPEG_files)
- [JPEG with Alpha](http://jim.studt.net/jpeg-alpha/) - Add add transparency data in `APPn` segment
- [ImpulseAdventure - Variable JPEG Compression](http://www.impulseadventure.com/photo/variable-compression.html)
- [ImpulseAdventure - JPEG Decoder Design](http://www.impulseadventure.com/photo/jpeg-decoder.html)
- [ImpulseAdventure - What is an Optimized JPEG?](http://www.impulseadventure.com/photo/optimized-jpeg.html)
- [ImpulseAdventure - JPEG Lossless Rotation with Partial MCU](http://www.impulseadventure.com/photo/rotation-partial-mcu.html)
- [ImpulseAdventure - JPEG Compression and JPEG Quality](http://www.impulseadventure.com/photo/jpeg-compression.html)
- [ImpulseAdventure - JPEG Quality and Quantization Tables for Digital Cameras, Photoshop](http://www.impulseadventure.com/photo/jpeg-quantization.html)
- [JPEGsnoop download | SourceForge.net](https://sourceforge.net/projects/jpegsnoop/) - see [ImpulseAdventure - JPEGsnoop 1.7.5 - JPEG Decoder Utility](http://www.impulseadventure.com/photo/jpeg-snoop.html)
- [How does JPEG actually work? – Developing for Developers](https://blogs.msdn.microsoft.com/devdev/2006/04/12/how-does-jpeg-actually-work/)
- [Kornel Lesiński | Image Optimization | performance.now() 2018 - YouTube](https://www.youtube.com/watch?v=jTXhYj2aCDU&start=66&end=616) - How JPEG works
- PDF uses JPEG2000
- [Unraveling The JPEG](https://parametric.press/issue-01/unraveling-the-jpeg/)
- [Finally understanding JPG – Compress-Or-Die](https://compress-or-die.com/Understanding-JPG/)

Luminance, Chroma Blue, Chroma Red

Subsampling:

- 4:4:4 (1×1) no subsampling (8×8 blocks)
- 4:2:2 (reduction by 2×1) horizontal shrink (16×8 blocks)
- 4:1:1
- 4:2:0 (reduction by 2×2) both axes (16×16 blocks)

### Compression

- [Fourier Transforms](http://www.jezzamon.com/fourier/index.html)
- [54- The JPEG compression algorithm - YouTube](https://www.youtube.com/watch?v=aFbGqXFT0Nw)
- [How JPEG Works - Computerphile - YouTube](https://www.youtube.com/playlist?list=PLzH6n4zXuckoAod3z31QEST1ZaizBuNHh)

## Grayscale

Note a dedicated format exist: 12-bit JPEG format, but this format is not as widely supported.

For grayscale JPEG, chroma components will be gray (50%)

	// Test grayscale image impact on luma (same as RGB source), chroma blue and chroma red (still grey)
	// That means for grayscale images chroma could be ignored or at least use the lower level of subsampling
	let canvas = document.createElement("canvas");
	canvas.width = 800;
	canvas.height = 400;
	let context = canvas.getContext("2d");
	var gradient = context.createRadialGradient(100, 100, 100, 100, 100, 80);
	gradient.addColorStop(0, 'black');
	gradient.addColorStop(1, 'white');
	context.fillStyle = gradient;
	context.fillRect(0, 0, 200, 200);
	let srcImageDataRaw = context.getImageData(0, 0, 200, 200).data;
	
	let lumaImageData = context.createImageData(200, 200);
	let lumaImageDataRaw = lumaImageData.data;
	let chromaBlueImageData = context.createImageData(200, 200);
	let chromaBlueImageDataRaw = chromaBlueImageData.data;
	let chromaRedImageData = context.createImageData(200, 200);
	let chromaRedImageDataRaw = chromaRedImageData.data;
	let testImageData = context.createImageData(200, 200);
	let testImageDataRaw = testImageData.data;
	// Separate each RGB pixels to YCbCr space (show side each channels)
	// https://en.wikipedia.org/wiki/YCbCr#JPEG_conversion
	for(let i = 0; i < srcImageDataRaw.length; i += 4/*RGBA*/){
		let srcRed = srcImageDataRaw[i];
		let srcGreen = srcImageDataRaw[i + 1];
		let srcBlue = srcImageDataRaw[i + 2];
	
		let luma = 0.299 * srcRed + 0.587 * srcGreen + 0.114 * srcBlue;
		lumaImageDataRaw[i] = lumaImageDataRaw[i + 1] = lumaImageDataRaw[i + 2] = Math.round(luma);
		lumaImageDataRaw[i + 3] = 0xFF;
	
		let chromaBlue = 0x80 - 0.168736 * srcRed - 0.331264 * srcGreen + 0.5 * srcBlue;
		chromaBlueImageDataRaw[i] = chromaBlueImageDataRaw[i + 1] = chromaBlueImageDataRaw[i + 2] = Math.round(chromaBlue);
		chromaBlueImageDataRaw[i + 3] = 0xFF;
	
		let chromaRed = 0x80 + 0.5 * srcRed - 0.418688 * srcGreen - 0.081312 * srcBlue;
		chromaRedImageDataRaw[i] = chromaRedImageDataRaw[i + 1] = chromaRedImageDataRaw[i + 2] = Math.round(chromaRed);
		chromaRedImageDataRaw[i + 3] = 0xFF;
	
		// Then revert YCbCr to RGB (to test it the computation is correct)
		let testRed = luma + 1.402 * (chromaRed  - 0x80);
		let testGreen = luma - 0.344136 * (chromaBlue - 0x80) - 0.714136 * (chromaRed  - 0x80);
		let testBlue = luma + 1.772 * (chromaBlue - 0x80);
		testImageDataRaw[i] = Math.round(testRed);
		testImageDataRaw[i + 1] = Math.round(testGreen);
		testImageDataRaw[i + 2] = Math.round(testBlue);
		testImageDataRaw[i + 3] = 0xFF;// alpha
	}
	
	context.putImageData(lumaImageData, 200, 0);
	context.putImageData(chromaBlueImageData, 400, 0);
	context.putImageData(chromaRedImageData, 600, 0);
	context.putImageData(testImageData, 0, 200);
	document.body.appendChild(canvas);

## Estimate quality

Via quantization tables.

- `jpegquality` by Neal Krawetz [Hacker Factor: Software](http://www.hackerfactor.com/software.php)
- [Marc Lehmann's "Judge"](http://oldhome.schmorp.de/marc/judge.html)
- [jpgQ Estimator](http://www.mediachance.com/digicam/jpgq.htm) - Judge makes an algorithmic analysis very similar to the jpeg compression algorithm, and then uses an heuristic to "guess" a quality factor between 0 and 1000.
- [ImpulseAdventure - JPEG Quality Comparison](http://www.impulseadventure.com/photo/jpeg-quality.html) and [ImpulseAdventure - JPEG Quality and Quantization Tables for Digital Cameras, Photoshop](http://www.impulseadventure.com/photo/jpeg-quantization.html)
- [Quantization Table Estimation in JPEG Images - Paper_3_Quantization_Table_Estimation_in_JPEG_Images_.pdf](http://thesai.org/Downloads/Volume1No6/Paper_3_Quantization_Table_Estimation_in_JPEG_Images_.pdf)
- [Image Quality Estimation for JPEG-Compressed Images without the Original Image](http://ivms.stanford.edu/~varodayan/mentorship/PetkovCottier.pdf)
- [IEEE Xplore Abstract - Identification of bitmap compression history: JPEG detection and quantizer estimation](http://ieeexplore.ieee.org/iel5/83/26748/01192984.pdf?arnumber=1192984)
- https://svn.xiph.org/experimental/giles/jpegdump.c
- [windows - How to find the JPG quality? - Super User](http://superuser.com/questions/62730/how-to-find-the-jpg-quality/91083#91083)
- [jpeg.c in ImageMagick/trunk/coders – ImageMagick](http://trac.imagemagick.org/browser/ImageMagick/trunk/coders/jpeg.c?rev=18089#L800)
- [Tutorial: Estimate JPEG Quality](http://fotoforensics.com/tutorial-estq.php)
- [Jpeg Compression - photo.net](http://photo.net/learn/jpeg/#jpegdmp)
- [XnView Software • View topic - Save JPG At 'Original' Quality](http://newsgroup.xnview.com/viewtopic.php?t=10298)
- [My Blog: JPEG quality is a meaningless number](http://patrakov.blogspot.fr/2008/12/jpeg-quality-is-meaningless-number.html)
- [Image Compression: How JPEG Works](http://nboddula.blogspot.fr/2013/05/image-compression-how-jpeg-works.html)
- [jpegtran fork with significant performance improvements](https://github.com/cloudflare/jpegtran)

## Compression optimization

> By default, JPEG will half the resolution of colour data, but you can disable this. You'll need to lower the overall quality to achieve the same file size, but the colours will stay sharper.
> \[...\] below 90% quality many encoders will default to 4:2:0 subsampling
> — [Jake Archibald on Twitter: "By default, JPEG will half the resolution of colour data, but you can disable this. You'll need to lower the overall quality to achieve the same file size, but the colours will stay sharper. https://t.co/N4XD3KFOvM Here's the original vs the JPEG too: https://t.co/g3mBJp68I9"](https://twitter.com/jaffathecake/status/1077881624765833218)

- [ImpulseAdventure - JPEG Huffman Coding Tutorial](http://www.impulseadventure.com/photo/jpeg-huffman-coding.html)
- [A Picture Costs A Thousand Words](http://www.slideshare.net/guypod/a-picture-costs-a-thousand-words18062013/15) - see [A picture costs a thousand words](./a-20picture-20costs-20a-20thousand-20words-130619124428-phpapp01.pdf#page15)
- [jpegcrush](http://akuvian.org/src/jpgcrush.tar.gz) (use jpegtran to trial many progressive configurations, same as JPEGrescan)
- [jpegoptim](https://github.com/glennr/jpegoptim)
- [png and jpg size optimization scripts](https://github.com/clyfish/pngopt)
- [jpegtran](http://jpegclub.org/jpegtran/)
- [JPEGrescan](https://github.com/kud/jpegrescan) (use jpegtran to trial many progressive configurations)
- [mozjpeg](https://github.com/mozilla/mozjpeg) (see also [the Thread about it on encode.su](https://encode.su/threads/1892-mozjpeg))
- [pingo, a fast image optimizer](http://css-ig.net/pingo)
- [adept-jpg-compressor](https://github.com/technopagan/adept-jpg-compressor) (equivalent to [JPEGMini](http://www.jpegmini.com/))
- https://github.com/danielgtaylor/jpeg-archive (JPEGmini like) using perceived visual quality
- [About jpegmini and similar compressors](https://encode.su/threads/1470-jpegmini-com)
- [imgmin](https://github.com/rflynn/imgmin) (could also compress PNG with supported tools like Pngnq, PNGCrush and PNGQuant)
- [JPGCrush](http://akuvian.org/src/jpgcrush.tar.gz) is a perl script written by Loren Merritt use jpegtran with differents options (see also [author's post on ExifTool Forum](http://u88.n24.queensu.ca/exiftool/forum/index.php?topic=3610.0) and [thread on Programmer's Town Forum](http://www.progtown.com/topic1198280-jpgcrush.html))
- [JSK -JPEG Scan Killer- progressive JPEG explained in slowmo](https://encode.su/threads/1800-JSK-JPEG-Scan-Killer-progressive-JPEG-explained-in-slowmo)
- [Clever JPEG Optimization Techniques](http://www.smashingmagazine.com/2009/07/01/clever-jpeg-optimization-techniques/)
- [JPEG Archive / JPEGmini like : compress JPEG by keeping perceived visual quality](https://github.com/danielgtaylor/jpeg-archive)
- [Comparison of jpeg optimisation tools | ImageOptim-CLI](http://jamiemason.github.io/ImageOptim-CLI/comparison/jpeg/photoshop/desc/)
- [Reducing JPG File size — Medium](https://medium.com/@duhroach/reducing-jpg-file-size-e5b27df3257c)
- https://github.com/technopagan/cjpeg-dssim
- https://github.com/technopagan/adept-jpg-compressor
- [Optimising JPEG compression by identifying image characteristics – Voormedia](http://voormedia.com/blog/2016/12/optimising-jpeg-image-compression-by-identifying-image-characteristics)
- [JPEG effets de bord et sous-échantillonnage chroma - YouTube](https://www.youtube.com/watch?v=V7LvgXqsh60) and [JPEG effets de bord et sous-échantillonnage chroma (suite) - YouTube](https://www.youtube.com/watch?v=pSp_MnXBOPg)
- [Performance Calendar » MozJPEG 3.0](https://calendar.perfplanet.com/2014/mozjpeg-3-0/)
- [Essential Image Optimization](https://images.guide/#the-humble-jpeg)

`convert -define jpeg:q-table=quantization-table.xml rgb_image.png image.jpg`, see [JPEG quantization tables and progressive scan scripts - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?f=2&t=20414&sid=8a1c6da472fcf63d7f0676b2a6b53db5)

		<?xml version="1.0" encoding="ISO-8859-1"?>
		<!DOCTYPE quantization-tables [
		<!ELEMENT quantization-tables (table)+>
		<!ELEMENT table (description , levels)>
		<!ELEMENT description (CDATA)>
		<!ELEMENT levels (CDATA)>
		<!ATTLIST table slot ID #REQUIRED>
		<!ATTLIST levels width CDATA #REQUIRED>
		<!ATTLIST levels height CDATA #REQUIRED>
		<!ATTLIST levels divisor CDATA #REQUIRED>
		]>
		<!--
		  JPEG quantization tables.
		-->
		<quantization-tables>
			<table slot="0" alias="luminance">
				<description>Luminance Quantization Table</description>
				<levels width="8" height="8" divisor="1">
					16, 12, 14, 17, 22, 30, 45, 72,
					12, 13, 14, 17, 22, 31, 46, 74,
					14, 14, 16, 19, 25, 35, 52, 83,
					17, 17, 19, 23, 30, 41, 62, 100,
					22, 22, 25, 30, 39, 54, 80, 129,
					30, 31, 35, 41, 54, 74, 111, 178,
					45, 46, 52, 62, 80, 111, 166, 267,
					72, 74, 83, 100, 129, 178, 267, 428
				</levels>
			</table>
		
			<table slot="1" alias="chrominance">
				<description>Chrominance Quantization Table</description>
				<levels width="8" height="8" divisor="1">
					17,  18,  22,  31,  50,  92,   193,  465,
					18,  19,  24,  33,  54,  98,   207,  498,
					22,  24,  29,  41,  66,  120,  253,  609,
					31,  33,  41,  57,  92,  169,  355,  854,
					50,  54,  66,  92,  148, 271,  570,  1370,
					92,  98,  120, 169, 271, 498,  1046, 2516,
					193, 207, 253, 355, 570, 1046, 2198, 5289,
					465, 498, 609, 854, 1370,2516, 5289, 12725
				</levels>
			</table>
		</quantization-tables>

- [JPEG — Wikipedia](https://en.wikipedia.org/wiki/JPEG#Lossless_further_compression) - Lossless further compression
- [packJPG | packJPG](https://web.archive.org/web/20180913135729/http://packjpg.encode.ru/?page_id=17) - see [packjpg/packJPG: A compression program for further compressing JPEG image files](https://github.com/packjpg/packJPG)

### Lossely compression

By default, JPEG will half the resolution of colour data, but you can disable this. You'll need to lower the overall quality to achieve the same file size, but the colours will stay sharper.

- [Lepton](https://github.com/dropbox/lepton)
	A tool and file format for losslessly compressing JPEGs by an average of 22%.
	
	- [Lepton image compression: saving 22% losslessly from images at 15MB/s | Dropbox Tech Blog](https://blogs.dropbox.com/tech/2016/07/lepton-image-compression-saving-22-losslessly-from-images-at-15mbs/)

### Selective compression

- [Optimisation JPEG: focalisation](http://css-ig.net/articles/optimisation-jpeg-focalisation)
- [senocular.com](http://www.senocular.com/fireworks/tutorials/mighthavemissed/#selectivejpeg)
- [technopagan/adept-jpg-compressor: A Bash script to automate adaptive JPEG compression using common CLI tools](https://github.com/technopagan/adept-jpg-compressor/)

Edit to blur the background to reduce weight: [Reducing image sizes — Responsive Web Design](https://responsivedesign.is/articles/reducing-image-sizes)

## Progressive scans

To check if it's progressive: `identify -verbose file.jpg | grep Interlace` should return `Interlace: JPEG`

	convert -interlace Plane source.jpg result.jpg

Number of scan and there configuration can be tweak/optimized

Optimal could be ([`cjpeg`](https://linux.die.net/man/1/cjpeg) scans script file, see `-scans`):

	# Initial DC for all channels (Y, Cb, Cr). Interleaved
	0,12:	0-0,	0,	1;
	# AC Scan
	0:		1-27,	0,	0; # Half of all brighter values.
	2:		1-63,	0,	0; # All remaining color channels.
	1:		1-63,	0,	0; # All remaining color channels.
	0:		28-63,	0,	0; # All remaining Y coefficients and half of brighter channel

- [Chris Hodapp's Blog - Obscure features of JPEG](https://hodapple.com/blag/posts/2011-11-24-obscure-features-of-jpeg.html)
- http://libjpeg.cvs.sourceforge.net/viewvc/libjpeg/libjpeg/wizard.doc?content-type=text%2Fplain
- [Tobias Baldauf — Your Hero Images Need You! Save the Day with HTTP2 Image Loading on Vimeo](https://vimeo.com/163113212#t=16m3s)
- [Your Hero Images Need You: Save the Day with HTTP/2 Image Loading - YouTube](https://www.youtube.com/watch?v=66JINbkBYqw)
- [Your Hero Images Need You! Save the Day with HTTP2 Image Loading - 90min Workshop at Velocity Santa Clara 2016 // Speaker Deck](https://speakerdeck.com/tbaldauf/your-hero-images-need-you-save-the-day-with-http2-image-loading-90min-workshop-at-velocity-santa-clara-2016)
- [Your Hero Images Need You! Save the Day with HTTP2 Image Loading // Speaker Deck](https://speakerdeck.com/tbaldauf/your-hero-images-need-you-save-the-day-with-http2-image-loading)
- [Your Hero Images Need You! Save the Day with HTTP2 Image Loading // Speaker Deck](https://speakerdeck.com/tbaldauf/your-hero-images-need-you-save-the-day-with-http2-image-loading-1)
- [Progressive jpeg tester](http://www.patrickmeenan.com/progressive/) (see also [sources on github](https://github.com/pmeenan/progressive-scans))
- [20160510-beyondtellerrand-DUS-h2-opjpeg.pdf](20160510-beyondtellerrand-DUS-h2-opjpeg.pdf)
- [Image Optimization, Part 4: Progressive JPEG...Hot or Not?](http://yuiblog.com/blog/2008/12/05/imageopt-4/)
- [Performance Calendar » MozJPEG 3.0](https://calendar.perfplanet.com/2014/mozjpeg-3-0/) - Define quant-table with MozJPEG. See also `-qtables` https://github.com/mozilla/mozjpeg/blob/master/wizard.txt

## Embedded clipping path

Photoshop: Window > Paths

	identify -format '%[8BIM:1999,2998:#1]' <myimage>

- https://stackoverflow.com/questions/3030577/is-it-possible-to-read-path-in-jpeg-image-with-python

## Decompression Bomb

A very big image with could take 12.88 GB (65535x65535x3) for uncompressed data from ~17MB of compressed data. `convert -size 65500x65500 xc:black canvas.jpg` (ImageMagick use libjpeg-turbo and [it has a limitation to 65500](http://superuser.com/questions/773356/why-does-imagemagicks-montage-limit-the-jpg-output-to-65500-instead-of-65535/773436#773436))

- [Decompression bomb protection · Issue #515 · python-pillow/Pillow](https://github.com/python-pillow/Pillow/issues/515)

## Orientation

Aka lossless orientation

Use it if you don't want to recompress the image data (quality loss)

See [Orientation](../EXIF/EXIF.md#orientation)
