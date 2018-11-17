Aka bicubic, bilinear, trilinear, lanczos interpolation, box filter, lanczos filter, hamming filter

Bilinear interpolation works better for size between 50% ≤ n ≤ 200%:

> Bilinear filtering is rather accurate until the scaling of the texture gets below half or above double the original size of the texture - that is, if the texture was 256 pixels in each direction, scaling it to below 128 or above 512 pixels can make the texture look bad, because of missing pixels or too much smoothness

Use it recursively to achieve a better result only with bilinear. See below.

Often used for image resizing or for perspective texture correction

- [How to upsize an image – Blog.forret.com](http://blog.forret.com/2006/08/23/how-to-upsize-an-image/)
- [Understanding Digital Image Interpolation](http://www.cambridgeincolour.com/tutorials/image-interpolation.htm)
- [Bilinear interpolation — Wikipedia](https://en.wikipedia.org/wiki/Bilinear_interpolation)
- [Interpolation (Introduction)](http://www.scratchapixel.com/lessons/mathematics-physics-for-computer-graphics/interpolation)
- GPU accelerated pre-filtered cubic b-spline interpolation
	- [CUDA Cubic B-Spline Interpolation (CI)](http://www.dannyruijters.nl/cubicinterpolation/)
	- [CUDA Cubic B-Spline Interpolation (CI) read me](http://www.dannyruijters.nl/cubicinterpolation/readme.html)
	- https://github.com/DannyRuijters/CubicInterpolationWebGL
	- https://github.com/DannyRuijters/CubicInterpolationCUDA
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/texture/texture.htm) - improved texture interpolation
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://iquilezles.org/www/articles/ibilinear/ibilinear.htm) - inverse bilinear interpolation
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/filtering/filtering.htm) - filtering procedural textures
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/hwinterpolation/hwinterpolation.htm) - hardware interpolation
- [Resampling volume or image with affine matrix - File Exchange - MATLAB Central](http://fr.mathworks.com/matlabcentral/fileexchange/21080-resampling-volume-or-image-with-affine-matrix) - see `affine.zip`
- [Tech-Algorithm.com ~ Bilinear Image Scaling](http://tech-algorithm.com/articles/bilinear-image-scaling/)
- [Tech-Algorithm.com ~ Trilinear Interpolation Image Scaling](http://tech-algorithm.com/articles/trilinear-interpolation-image-scaling/)
- [Chapter 6. Resampling](http://pippin.gimp.org/image_processing/chap_resampling.html)
- [Cubic interpolation - Paulinternet.nl](http://www.paulinternet.nl/?page=bicubic) - Java and C++ Implementations
- [Réduction de BitmapData & Smoothing : Pourquoi c'est pas beau (et comment améliorer) - envrac.org](http://wayback.archive.org/web/20110903152621/http://www.envrac.org/index.php/2008/06/23/181-reduction-de-bitmapdata-smoothing-pourquoi-c-est-pas-beau-et-comment-ameliorer) - use bilinear iteratively/recursively using `scale * 2` until final size:
	See `BitmapManager.as`
	
		public static function resampleBitmapData (bmp:BitmapData, ratio:Number):BitmapData {
			if (ratio >= 1) {
				return (BitmapManager.resizeBitmapData(bmp, ratio));//do bilinear resample
			}
			else {
				var bmpData:BitmapData = bmp.clone();
				var appliedRatio:Number = 1;
		
				do {
					if (ratio < 0.5 * appliedRatio) {
						bmpData = BitmapManager.resizeBitmapData(bmpData, 0.5);
						appliedRatio = 0.5 * appliedRatio;
					}
					else {
						bmpData = BitmapManager.resizeBitmapData(bmpData, ratio / appliedRatio);
						appliedRatio = ratio;
					}
				} while (appliedRatio != ratio);
		
				return (bmpData);
			}
		}
	
	See [How to resize an image with ActionScript (update) at Jozef Chúťka's blog](http://blog.yoz.sk/2010/01/how-to-resize-an-image-with-actionscript/)
- [b4wind User's Guide - Interpolation](https://www.grc.nasa.gov/WWW/winddocs/utilities/b4wind_guide/interpolation.html) and [b4wind User's Guide - Trilinear Interpolation](https://www.grc.nasa.gov/WWW/winddocs/utilities/b4wind_guide/trilinear.html)
- [Bicubic resampling by Pixel Bender - Andy Li’s Blog](https://blog.onthewings.net/2009/08/25/bicubic-resampling-by-pixel-bender/)
- [geographic data processing engine for high performance applications](https://github.com/locationtech/geotrellis/tree/master/raster/src/main/scala/geotrellis/raster/resample) - resample algorithms of scala lib. See the geotrellis-raster module
- [Lanczos Resampling - wonderfl build flash online](http://wonderfl.net/c/dLf0) - see [Lanczos Resampling With ActionScript at Jozef Chúťka's blog](http://blog.yoz.sk/2010/11/lanczos-resampling-with-actionscript/)
- [algorithm - Where can I find a good read about bicubic interpolation and Lanczos resampling? - Stack Overflow](https://stackoverflow.com/questions/943781/where-can-i-find-a-good-read-about-bicubic-interpolation-and-lanczos-resampling)
- [Source | SVN | Assembla](https://app.assembla.com/spaces/sk-yoz-classes/subversion/source/HEAD/trunk/src)
- https://chromium.googlesource.com/chromium/src/+/master/skia/ext/image_operations.cc - see EvalBox, EvalLanczos, EvalHamming
- [Resampling Filters -- IM v6 Examples](http://www.imagemagick.org/Usage/filter/) - https://github.com/ImageMagick/ImageMagick/blob/master/MagickCore/resize.c see also [ImageMagick scaling algorithms](http://www.robotplanet.dk/graphics/imagemagick_scaling/)

## Correct color interpolation

Aka correct color blending

> of course nobody is using it - three sqrt per pixel

	// From http://codepen.io/quasimondo/pen/VLaYjx Correct Color Blending
	var width = 1600;
	var colorLeft = 0x8f3080;
	var colorRight = 0xc0ff00;
	
	
	function blendColorsCorrectly(a, b, data) {
		var ar = (a >> 16) & 0xff;
		ar *= ar;
		var ag = (a >> 8) & 0xff;
		ag *= ag;
		var ab = a & 0xff;
		ab *= ab;
		
		var br = (b >> 16) & 0xff;
		br *= br;
		var bg = (b >> 8) & 0xff;
		bg *= bg;
		var bb = b & 0xff;
		bb *= bb;
		
		var l = data.length;
		var il = 1 / (l*l);
		for (var i = 0; i < l; i++) 
		{
			var li = (l-1)-i;
			var r = (0.5 + Math.sqrt(il * (li*li * ar + i * i *br))) | 0;
			var g = (0.5 + Math.sqrt(il * (li*li * ag + i * i *bg))) | 0;
			var b = (0.5 + Math.sqrt(il * (li*li * ab + i * i *bb))) | 0;
			data[i] = 0xff000000 | r << 16 | g << 8 | b;
		}
		return data;
	}
	
	function blendColorsIncorrectly(a, b, data) {
		var ar = (a >> 16) & 0xff;
		var ag = (a >> 8) & 0xff;
		var ab = a & 0xff;
		var br = (b >> 16) & 0xff;
		var bg = (b >> 8) & 0xff;
		var bb = b & 0xff;
		
		var l = data.length;
		var il = 1 / l;
		for (var i = 0; i < l; i++) 
		{
			var r = (0.5 + (il * ((l-1-i) * ar + i * br))) | 0;
			var g = (0.5 + (il * ((l-1-i) * ag + i * bg))) | 0;
			var b = (0.5 + (il * ((l-1-i) * ab + i * bb))) | 0;
			data[i] = 0xff000000 | r << 16 | g << 8 | b;
		
		}
		return data;
	}
	
	var buffer = new ArrayBuffer(width * 4);
	var u32 = new Uint32Array(buffer);
	var u8 = new Uint8ClampedArray(buffer);
	var canvas = document.createElement("canvas");
	canvas.width = width;
	canvas.height = 200;
	document.body.appendChild(canvas);
	var ctx = canvas.getContext("2d");
	var imgData = ctx.getImageData(0, 0, width, 200);
	
	blendColorsCorrectly(colorLeft, colorRight, u32);
	for (var i = 0; i < 100; i++) {
		imgData.data.set(u8, i * width * 4);
	}
	
	blendColorsIncorrectly(colorLeft, colorRight, u32);
	for (var i = 100; i < 200; i++) {
		imgData.data.set(u8, i * width * 4);
	}
	ctx.putImageData(imgData, 0, 0);

- [Computer Color is Broken - YouTube](https://www.youtube.com/watch?v=LKnqECcg6Gw)
- https://twitter.com/quasimondo/status/598174439314972673