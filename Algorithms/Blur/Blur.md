Aka drop shadow

See [Deblur](Deblur)

- [Blur](http://blackpawn.com/texts/blur/default.html)
- [Java Image Processing - Blurring for Beginners](http://www.jhlabs.com/ip/blurring.html)
- [Zack Rusin: More blurring](http://zrusin.blogspot.com/2006/07/more-blurring.html)
- [v002 Blurs 2.0.2 | v002](http://v002.info/plugins/v002-blurs/)
- [Linear and Radial Blur with HTML5 | Pixelero](https://pixelero.wordpress.com/2014/12/15/linear-and-radial-blur-with-html5/) and [Pixel Bender: Blur with Linear Focus | Pixelero](https://pixelero.wordpress.com/2008/08/28/pixel-bender-blur-with-linear-focus/)
- [glfx.js](http://evanw.github.io/glfx.js/demo/) - An image effects library for JavaScript using WebGL. See https://github.com/evanw/glfx.js (and [WebGL Filter](http://evanw.github.io/webgl-filter/), https://github.com/evanw/webgl-filter/)
- [Drawing CSS Box Shadows in WebRender - pcwalton](http://pcwalton.github.io/blog/2015/12/21/drawing-css-box-shadows-in-webrender/)

## Correct color interpolation

See [correct color interpolation](Interpolation#Correct color interpolation)

## Radial blur

- [Quasimondo - Mario Klingemann's Flash Blog: Fast Radial Blur](http://www.quasimondo.com/archives/000697.php)

## Gaussian blur

Often use 2 passes:

1. blur horizontally
2. blur vertically

- [Gaussian blur — Wikipedia](https://en.wikipedia.org/wiki/Gaussian_blur)
- [Shader Lesson 5](https://github.com/mattdesl/lwjgl-basics/wiki/ShaderLesson5) - Detailed infos about gaussian blur multi passes implementation using GLSL with Frame Buffer Object (FBO)
- [glsl-fast-gaussian-blur](http://jam3.github.io/glsl-fast-gaussian-blur/) - See [Optimized separable gaussian blurs for GLSL](https://github.com/Jam3/glsl-fast-gaussian-blur). Use [Efficient Gaussian blur with linear sampling](http://rastergrid.com/blog/2010/09/efficient-gaussian-blur-with-linear-sampling/)
- [Gaussian blur demo](https://www.nayuki.io/page/gaussian-blur-demo) - See https://www.nayuki.io/res/gaussian-blur-demo/gaussian-blur-demo.js
- [Bloom](https://learnopengl.com/#!Advanced-Lighting/Bloom)
- [stereopsis : Fast Shadows on Rectangles](http://stereopsis.com/shadowrect/)

### Fast gaussian blur

- [Quasimondo : Incubator : Processing : Fast Gaussian Blur](http://incubator.quasimondo.com/processing/gaussian_blur_1.php) - see http://incubator.quasimondo.com/processing/fastblur.pde

## Integral blur

## Stack blur

- [StackBlur - A fast, almost Gaussian blur for Canvas by Mario Klingemann, Quasimondo](http://www.quasimondo.com/StackBlurForCanvas/StackBlurDemo.html)
- [Quasimondo : Incubator : Processing : Stack Blur](http://incubator.quasimondo.com/processing/fast_blur_deluxe.php)

## Box blur

- [StackBoxBlur - A pretty fast Box Blur for Canvas by Mario Klingemann, Quasimondo](http://www.quasimondo.com/BoxBlurForCanvas/FastBlur2Demo.html)

### Superfast box blur

> It may not look as beautiful as a Gaussian blur, but I think that a box blur can't get any faster than this. The specialty about this algorithm is that its speed is almost independent of the used radius. This works, because the convolution kernel is not recalculated on each pixel: scanning through the image the algorithm just adds one new pixel to the kernel and at the same time drops one old pixel from it.
> 
> The "iterations" argument controls how many times the blur will be repeated. This can be used to achieve a smoother look, but it will slow down things considerably especially for big radii. I rather recommend to use StackBlur in that case.

- [Superfast Blur - A pretty fast box blur for Canvas by Mario Klingemann, Quasimondo](http://www.quasimondo.com/BoxBlurForCanvas/FastBlurDemo.html)
- [Quasimondo : Incubator : Processing : Superfast Blur](http://incubator.quasimondo.com/processing/superfast_blur.php)

## Shadow Blur

- https://github.com/ariya/X2/blob/master/graphics/shadowblur/shadowblur.cpp
- [the art of blurring the shadow · ariya.io](https://ariya.io/2010/09/the-art-of-blurring-the-shadow)
 
	/*
	  This file is part of the Ofi Labs X2 project.
	
	  Copyright (C) 2010 Ariya Hidayat <ariya.hidayat@gmail.com>
	
	  Redistribution and use in source and binary forms, with or without
	  modification, are permitted provided that the following conditions are met:
	
	    * Redistributions of source code must retain the above copyright
	      notice, this list of conditions and the following disclaimer.
	    * Redistributions in binary form must reproduce the above copyright
	      notice, this list of conditions and the following disclaimer in the
	      documentation and/or other materials provided with the distribution.
	    * Neither the name of the <organization> nor the
	      names of its contributors may be used to endorse or promote products
	      derived from this software without specific prior written permission.
	
	  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
	  AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
	  IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
	  ARE DISCLAIMED. IN NO EVENT SHALL <COPYRIGHT HOLDER> BE LIABLE FOR ANY
	  DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
	  (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
	  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
	  ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
	  (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
	  THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
	*/
	
	#include "shadowblur.h"
	
	#include <QImage>
	#include <QPainter>
	
	static const int BlurSumShift = 15;
	
	// Check http://www.w3.org/TR/SVG/filters.html#feGaussianBlur.
	// As noted in the SVG filter specification, running box blur 3x
	// approximates a real gaussian blur nicely.
	
	void shadowBlur(QImage& image, int radius, const QColor& shadowColor)
	{
	    // See comments in http://webkit.org/b/40793, it seems sensible
	    // to follow Skia's limit of 128 pixels for the blur radius.
	    if (radius > 128)
	        radius = 128;
	
	    int channels[4] = { 3, 0, 1, 3 };
	    int dmax = radius >> 1;
	    int dmin = dmax - 1 + (radius & 1);
	    if (dmin < 0)
	        dmin = 0;
	
	    // Two stages: horizontal and vertical
	    for (int k = 0; k < 2; ++k) {
	
	        unsigned char* pixels = image.bits();
	        int stride = (k == 0) ? 4 : image.bytesPerLine();
	        int delta = (k == 0) ? image.bytesPerLine() : 4;
	        int jfinal = (k == 0) ? image.height() : image.width();
	        int dim = (k == 0) ? image.width() : image.height();
	
	        for (int j = 0; j < jfinal; ++j, pixels += delta) {
	
	            // For each step, we blur the alpha in a channel and store the result
	            // in another channel for the subsequent step.
	            // We use sliding window algorithm to accumulate the alpha values.
	            // This is much more efficient than computing the sum of each pixels
	            // covered by the box kernel size for each x.
	
	            for (int step = 0; step < 3; ++step) {
	                int side1 = (step == 0) ? dmin : dmax;
	                int side2 = (step == 1) ? dmin : dmax;
	                int pixelCount = side1 + 1 + side2;
	                int invCount = ((1 << BlurSumShift) + pixelCount - 1) / pixelCount;
	                int ofs = 1 + side2;
	                int alpha1 = pixels[channels[step]];
	                int alpha2 = pixels[(dim - 1) * stride + channels[step]];
	                unsigned char* ptr = pixels + channels[step + 1];
	                unsigned char* prev = pixels + stride + channels[step];
	                unsigned char* next = pixels + ofs * stride + channels[step];
	
	                int i;
	                int sum = side1 * alpha1 + alpha1;
	                int limit = (dim < side2 + 1) ? dim : side2 + 1;
	                for (i = 1; i < limit; ++i, prev += stride)
	                    sum += *prev;
	                if (limit <= side2)
	                    sum += (side2 - limit + 1) * alpha2;
	
	                limit = (side1 < dim) ? side1 : dim;
	                for (i = 0; i < limit; ptr += stride, next += stride, ++i, ++ofs) {
	                    *ptr = (sum * invCount) >> BlurSumShift;
	                    sum += ((ofs < dim) ? *next : alpha2) - alpha1;
	                }
	                prev = pixels + channels[step];
	                for (; ofs < dim; ptr += stride, prev += stride, next += stride, ++i, ++ofs) {
	                    *ptr = (sum * invCount) >> BlurSumShift;
	                    sum += (*next) - (*prev);
	                }
	                for (; i < dim; ptr += stride, prev += stride, ++i) {
	                    *ptr = (sum * invCount) >> BlurSumShift;
	                    sum += alpha2 - (*prev);
	                }
	            }
	        }
	    }
		
	    // "Colorize" with the right shadow color.
	    QPainter p(&image);
	    p.setCompositionMode(QPainter::CompositionMode_SourceIn);
	    p.fillRect(image.rect(), shadowColor);
	    p.end();
	}

## Motion blur

- [Analytical Motionblur 3D](https://www.shadertoy.com/view/MdB3Dw) - see also "Sphere Motion" [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/spherefunctions/spherefunctions.htm)