## Resources

See also [Compare image](Compare data#Compare image)

`identify -verbose image.ext`

Libraires support differents formats

- [DevIL - A full featured cross-platform Image Library](http://openil.sourceforge.net/) - cross-platform image library utilizing a simple syntax to load, save, convert, manipulate, filter, and display a variety of images. See [Developer's Image Library (DevIL)](https://github.com/DentonW/DevIL)
	Support lot of image formats (loading 40+). See https://github.com/DentonW/DevIL/tree/master/DevIL/src-IL/src

	See also [ResIL](https://sourceforge.net/projects/resil/), a supposed DevIL sucessor
- [Book of Speed](http://www.bookofspeed.com/chapter5.html) - Optimizing Images
- [FRDX - PNG vs WebP](http://frdx.free.fr/png_vs_webp.htm)
- [File:Felis silvestris silvestris small gradual decrease of quality.png — Wikipedia](https://en.wikipedia.org/wiki/File:Felis_silvestris_silvestris_small_gradual_decrease_of_quality.png)
- [Essential Image Optimization](https://images.guide/)

Responsive image (use JPEG): [Responsive Image Container · Yoav Weiss](https://blog.yoav.ws/responsive_image_container/). See https://github.com/yoavweiss/Responsive-Image-Container

## Use video codec

1 frame video

Exemple: H.264 image (video as image):

	ffmpeg.exe -i image.jpg -an -vcodec libx264 -coder 1 -flags +loop -cmp +chroma -subq 10 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -flags2 +dct8x8 -trellis 2 -partitions +parti8x8+parti4x4 -crf 24 -threads 0 -r 25 -g 25 -y image.mp4

The `-crf` parameter changes the quality level. Try with values from 15 to 30 (the final effect depends by frame size). You can also resize the frame prior to encode using the parameter `-s WxH` (es: `-s 640×360`).

- [H.264 for image compression | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2010/10/19/h-264-for-image-compression/)

See also WebP, a specific container for 1 frame (animation are also supported) use VP8 codec and inspirated from the WebM container

## Animated image

Use format like APNG or Animated WebP, looped video or GIF
See also MNG.

It's depend usage: APNG flat animation, vector rendered, etc. WebP is more for moving content like photo (video)

- [GIF vs APNG vs WebP](http://littlesvr.ca/apng/gif_apng_webp.html)

## Compression and optimisation

- [List of compression/optimisation tools and advices](http://addyosmani.com/blog/image-optimization-tools/) (most of them listed here)
- [ImageOptim](http://imageoptim.com/) (OSX GUI)
- [ImageAlpha](http://pngmini.com/lossypng.html) (OSX GUI)
- [Yahoo Smush.it](http://www.smushit.com/ysmush.it/) (online tool)
- [Image Compression for Web Developers](http://www.html5rocks.com/en/tutorials/speed/img-compression/)
- [Diary Of An x264 Developer » H.264 and VP8 for still image coding: WebP?](http://x264dev.multimedia.cx/archives/541)
- [Comparison of all optimisation tools | ImageOptim-CLI](http://jamiemason.github.io/ImageOptim-CLI/comparison/all/photoshop/desc/)
- [Image Compression for Web Developers - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/img-compression/)

Manally optimizations:

- [Clever PNG Optimization Techniques – Smashing Magazine](https://www.smashingmagazine.com/2009/07/clever-png-optimization-techniques/)
- [Clever JPEG Optimization Techniques – Smashing Magazine](https://www.smashingmagazine.com/2009/07/clever-jpeg-optimization-techniques/)

Use an influence mask (part that need less compression that others)

### Spritesheet

Regroup image inside file, mutualize header, compression codec, metadata, etc.

### Monochrome image compression

Use a RGBA container like PNG and encode 4 monochrome image in each color channel. A spritesheet with each channels.

Be carefull with alpha, some applications replace full transparent pixels with black transparent (don't keep RGB data).

You can use PNG8 by reduce color.

### Compression by downscaling

Aka retina revolution

**Not adviced due to ×4 memory usage**

> More detail with less kilobytes

Image with resolution ×2 but with an highly lossy compression like JPEG 0%.
But can require more process and more memory.

Example:

- Default: 300px / jpg quality 80 / 21kb
- Better quality: 600px / jpg quality 42 / 21kb

For JPEG it's better for quality above 90% (non scaled image with Q > 90% are better)

- [Compressive Image Revisited - TimKadlec.com](https://timkadlec.com/remembers/2018-03-22-compressive-images-revisited/)
- [Retina revolution - Netvlies](https://www.netvlies.nl/tips-updates/design-interactie/design-interactie/retina-revolution/) - [Retina Revolution - smaller images with better quality | Hacker News](https://news.ycombinator.com/item?id=4623160)
- [Retina revolutie follow up - Netvlies](https://www.netvlies.nl/tips-updates/algemeen/algemeen/retina-revolutie-follow-up/)
- [Compressive Images | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/compressive-images.html)
- [Retina Trick ou Compressive Images : des images en haute résolution partout - Alsacreations](https://www.alsacreations.com/astuce/lire/1730-retina-trick-compressive-images-resolution-picture-img-srcset-responsive.html)
- [Image Compression for Web Developers - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/img-compression/)
- [Reducing JPG File size – Colt McAnlis – Medium](https://medium.com/@duhroach/reducing-jpg-file-size-e5b27df3257c)
- [JPEG Compression: Is 80 the magic quality - Part 1 - the retina screens - pieroxy.net](http://pieroxy.net/blog/2016/05/01/jpeg_compression_is_80_the_magic_quality_part_1_the_retina_screens.html)
- [Do Retina Images Really Mean Larger Files? | Humanising the Digital](http://alidark.com/responsive-retina-image-mobile/)
- [JPEG compression and retina displays](https://www.hdevalence.ca/blog/2013-04-09-JPEG-compression-and-retina-displays)
- [Resizing for Retina](http://wayback.archive.org/web/20121105033948/http://silev.org:80/test/Retina-resize.html)

### Alpha compression

Hybrid/Combined format (or container) to encode color channel in a format and transparency in other

See also [JPEG XR](https://en.wikipedia.org/wiki/JPEG_XR)

- Texture format ETC1 + ETC1 See [Texture format](Texture format)

#### Side by side channels

Aka atlas of RGB and Alpha as "black and white". This makes the image wider or taller.

Note: For image formats that use chrominance compression (like JPEG) this will **use the luminance channel (Y) only**. Cb & Cr will have all pixels grey, equal to 0.5 (for float value or 128 for 8bit values, in range of [0...255]) and are not required. See how [JNG](#JNG) works

#### Pre-multiplied alpha

Bink's premultiplied alpha video compression

- [Bink Video Alpha](http://www.radgametools.com/binkalpha.htm) (archive: https://archive.is/http://www.radgametools.com/binkalpha.htm)

#### WebP with Alpha Channel

- [Libwebp Javascript - HTML5 Offline WebP Decoder & Encoder](http://libwebpjs.appspot.com/)
- [WebPJS - Google's new image format WebP for not supported browsers (with alpha-channel)](http://webpjs.appspot.com/)
- https://github.com/antimatter15/weppy

And derived support of WebM with Alpha Channel

- In AE RGB (Output Module Settings > Main Options > Video Ouput > Channels) and Alpha as 2 sequences and make a composition with both in same times, then in JS merge part 1 RGB + part 2 R as RGBA: [HTML5 Video with alpha transparency](http://www.sciencelifeny.com/transparency/transparency.html)
- https://github.com/m90/seeThru

#### JNG

> JNG is a JPEG-based graphics file format which is closely related to PNG: it uses the PNG file structure (with a different signature) as a container format to wrap JPEG-encoded image data.
> [...] JNG files embed an 8-bit or 12-bit JPEG datastream in order to store color data, and may embed another datastream (1, 2, 4, 8, 16-bit PNG, or 8-bit JPEG grayscale image) for transparency information
— [JPEG Network Graphics — Wikipedia](https://en.wikipedia.org/wiki/JPEG_Network_Graphics)

`image/x-jng`

- [MNG (Multiple-image Network Graphics) Home Page](http://www.libpng.org/pub/mng/)

#### MNG

`video/x-mng`

- [MNG (Multiple-image Network Graphics) Home Page](http://www.libpng.org/pub/mng/)

#### SVG with JPEG

It's better to embed with data URI for independancy, but add weight (4/3%)

	<svg viewBox="0 0 500 400">
		<defs>
			<clipPath id="clip">
				<path d="..." />
			</clipPath>
		</defs>
		<image xlink:href="..." clip-path="url(#clip)" x="0" y="0" width="500" height="400">
	<svg>

- [ZorroSVG - Put a Mask on it](http://quasimondo.com/ZorroSVG/) - use JEPG to contains both RGB and Alpha channels in top-down order (side by side, RGB to top and alpha to bottom, as black and white)
- [Transparent JPG (With SVG) | CSS-Tricks](https://css-tricks.com/transparent-jpg-svg/)

#### SVG with JPEG + PNG

It's better to embed both files with data URI for independancy, but add weight (4/3%)

Use mask (black and white)

- [Applying Alpha Channels to JPGs | eleqtriq](http://w3.eleqtriq.com/2014/08/applying-alpha-channels-to-jpgs/)
- [Using SVG to shrink your PNGs | Peter Hrynkow](http://peterhrynkow.com/how-to-compress-a-png-like-a-jpeg/)

#### JPEG + PNG8 or JPEG + gray scale JPEG

Or JPEG + PNG1(w/ tRNS)

	// Merges the rgb channels of one image with the alpha channel of another
	ctx.save();
	ctx.drawImage(rgbImage, 0, 0);
	ctx.globalCompositeOperation = "destination-in";
	ctx.drawImage(alphaImage, 0, 0);
	ctx.restore();

Other possibilities:

	ctx.save();
	ctx.drawImage(rgbImage, 0, 0);
	ctx.globalCompositeOperation = "xor";
	ctx.drawImage(inverseAlphaMask, 0, 0);// black image with transparent pixel where rbgImage will be visible
	ctx.restore();

	// Will create an inverse alpha mask from grey-scale image (black and white)
	var alpha = document.createElement("canvas");
	alpha.width = alphaChannelImage.naturalWidth || alphaChannelImage.width;
	alpha.height = alphaChannelImage.naturalHeight || alphaChannelImage.height;
	var actx = alpha.getContext("2d");
	actx.drawImage(alphaChannelImage, 0, 0);
	var id = actx.getImageData(0, 0, alpha.width, alpha.height);
	var data = id.data;
	for (var i = 0; i < data.length - 4; i += 4) {
		data[i + 3] = 255 - data[i];// copy the inverse of the red channel to the alpha channel
	}
	actx.putImageData(id, 0, 0);
	
	ctx.save();
	ctx.drawImage(rgbImage, 0, 0);
	ctx.globalCompositeOperation = "xor";
	ctx.drawImage(alpha, 0, 0);// black image with transparent pixel where rbgImage will be visible
	ctx.restore();

- [Adding alpha channels or chroma keys to JPEG images | W3C Blog](http://www.w3.org/blog/2013/03/adding-alpha-channels-or-chrom/)
- [Reducing File Size for Images With Alpha Channels - gskinner blog](http://blog.gskinner.com/archives/2012/08/reducing-file-size-for-images-with-alpha-channels.html)
- [Emulating Lossy RGBA Images with HTML5's Canvas Element](http://kaioa.com/node/104)
- [javascript - Canvas: mask an image and preserve its alpha channel? - Stack Overflow](https://stackoverflow.com/questions/9032050/canvas-mask-an-image-and-preserve-its-alpha-channel)

#### JPEG with embedded alpha channel

In an `APPn` segment.

See [JPEG format](JPEG#format)

- [JPEG with Alpha](http://jim.studt.net/jpeg-alpha/)

#### Multipage TIFF

- https://github.com/GPHemsley/tiff-js
- https://github.com/GPHemsley/pdf.js/blob/tiff.js/src/tiff_core.js
- [tiffus - Binary image manipulation library for client side Google Web Toolkit JAVA and JavaScript - Google Project Hosting](https://code.google.com/p/tiffus/)
- https://github.com/seikichi/tiff.js

- https://github.com/netroy/image-size/blob/master/lib/types/tiff.js

### Selective/perceptual compression

Only available in Fireworks. Removed in Photoshop CS4.

- [Optimisation JPEG: focalisation](http://css-ig.net/articles/optimisation-jpeg-focalisation)
- [Macromedia Fireworks - Selectively compressing areas of an image: Create a selective JPEG mask](https://www.adobe.com/support/fireworks/workpixels/selective_jpeg/selective_jpeg02.html)
- [PS 300: Save for web and devices](http://phsh.ro/moodle/mod/page/view.php?id=43)
- [Advanced Image Optimization Tricks | Hacker News](https://news.ycombinator.com/item?id=6958729)
- [selections - How do you export a jpeg with a selective compression mask from Photoshop CC 2014? - Graphic Design Stack Exchange](http://graphicdesign.stackexchange.com/questions/41912/how-do-you-export-a-jpeg-with-a-selective-compression-mask-from-photoshop-cc-201)
- [File:Felis silvestris silvestris small gradual decrease of quality.png - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/File:Felis_silvestris_silvestris_small_gradual_decrease_of_quality.png)

### Others techniques

And pixel aligned on [8×8 JPEG macroblock/grid](https://stackoverflow.com/questions/10780425/why-jpeg-compression-processes-image-by-8x8-blocks) or PNG [deflate windows](PNG#deflate). Blur, reduce number of colors ([Posterization](http://en.wikipedia.org/wiki/Posterization)), [add noise](http://coding.smashingmagazine.com/2011/08/30/optimize-images-with-html5-canvas/)

- [Оптимизация JPEG. Часть первая](http://www.artlebedev.ru/tools/technogrette/img/jpeg-1/)
- [Clever JPEG Optimization Techniques - Smashing Magazine](http://www.smashingmagazine.com/2009/07/01/clever-jpeg-optimization-techniques/)
- [Pourquoi 1 pixel peut-il tout changer](http://css-ig.net/articles/pourquoi-1-pixel-change-tout)
- [Advanced Image Optimization Tricks](http://sixrevisions.com/web-development/advanced-image-optimization/)
- [Pixel-fitting](http://dcurt.is/pixel-fitting)

### Remove headers

For image with same size and same palette / same DCT coefficients - quant tables (JPEG)

### Post processing

Sharpen focus/important protions: High Pass filter (+ Soft Light or Hard Light)

- [waifu2x-multi](http://waifu2x.me/)

## Metadata

See [EXIF](EXIF), [IPTC](IPTC) and [XMP](XMP)

Remove all metadata:

With [ExifTool by Phil Harvey](http://www.sno.phy.queensu.ca/~phil/exiftool/):

	exiftool -gps:all= -xmp-exif:all= image.jpg

With [ImageMagick](http://www.imagemagick.org/script/index.php):

	mogrify -strip image.jpg

Note: use ImageMagick re-encode JPEG image data, see [unix - How to remove EXIF data without recompressing the JPEG? - Stack Overflow](https://stackoverflow.com/questions/2654281/how-to-remove-exif-data-without-recompressing-the-jpeg#comment2670770_2654371)

- ImageMagick `-comment` option [ImageMagick: Command-line Options](http://www.imagemagick.org/script/command-line-options.php#comment)
- [Metadata Analysis](http://fotoforensics.com/tutorial-meta.php)
- [Exiv2 - Image metadata library and tools](http://www.exiv2.org/) - A C++ library and a command line utility to easly read and write Exif, IPTC and XMP metadata
- [exif-js/exif-js: JavaScript library for reading EXIF image metadata](https://github.com/exif-js/exif-js) - EXIF and IPTC

Get the size from header:

- [Node.JS module for detecting image dimensions](https://github.com/image-size/image-size) - BMP, GIF, JPG, PNG, PSD, SVG, TIFF, WebP
- [measure image size(GIF, PNG, JPEG, etc.)](https://github.com/dabble/imagesize) - PCX, PSD, XPM, TIFF, XBM, PGM, PBM, PPM, BMP, JPEG, PNG, GIF, SWF
- [Get image size without full download](https://github.com/nodeca/probe-image-size) - JPG, GIF, PNG, WebP, BMP, TIFF, SVG, PSD
- https://sourceforge.net/p/exiftool/code/ci/master/tree/lib/Image/ExifTool/

## Convert

- [ImageMagick](https://www.imagemagick.org/script/index.php)
- Bitmap to vector with [Potrace](http://potrace.sourceforge.net/)