- [Color space — Wikipedia](https://en.wikipedia.org/wiki/Color_space)
- [HSL and HSV — Wikipedia](https://en.wikipedia.org/wiki/HSL_and_HSV)
- [YCbCr — Wikipedia](https://en.wikipedia.org/wiki/YCbCr)
- [RGB/XYZ Matrices](http://www.brucelindbloom.com/index.html?Eqn_RGB_XYZ_Matrix.html)
- [YCC colour space and image compression](http://wayback.archive.org/web/20120415141410/http://local.wasp.uwa.edu.au/~pbourke//texture_colour/ycc/)
- [Les espaces de couleur](http://wayback.archive.org/web/20080318070552/http://www.tsi.enst.fr/tsi/enseignement/ressources/mti/RVB_ou_LAB/html/colorspace.html)
- [Color Conversion Algorithms](https://www.cs.rit.edu/~ncs/color/t_convert.html)
- [EasyRGB - The inimitable RGB and COLOR search engine!](http://www.easyrgb.com/index.php?X=MATH)
- [Debian -- Détails du paquet libgraphics-colorobject-perl dans sid](https://packages.debian.org/unstable/perl/libgraphics-colorobject-perl)
- [On hue subdividision for mortals · ariya.io](https://ariya.io/2009/04/on-hue-subdividision-for-mortals)
- [bourkeYCrCbCompressionExperiment](http://timmaffett.com/source/bourkeYCrCbCompressionExperiment.html) - Paul Bourke's YCrCb compression using Flash 8's filters. See http://timmaffett.com/source/bourkeYCrCb.zip
- [HSL and HSV — Wikipedia](https://en.wikipedia.org/wiki/HSL_and_HSV#Converting_to_RGB) - RGB to/from HSL/HSV
- [Quasimondo - Mario Klingemann's Flash Blog: Converting RGB to HSL differently](http://www.quasimondo.com/archives/000696.php) - RGB-HSL approximation (use it only for real-time)
- [Gamma FAQ - Abstract](http://www.poynton.com/GammaFAQ.html) - Frequently-Asked Questions about Gamma. See http://www.poynton.com/PDFs/GammaFAQ.pdf
- [Color FAQ - Abstract](http://www.poynton.com/ColorFAQ.html) - Frequently Asked Questions about Colour (Color). See http://www.poynton.com/PDFs/ColorFAQ.pdf
- [Color: From Hexcodes to Eyeballs](http://jamie-wong.com/post/color/#color-spaces)
- [Color JS library](https://gist.github.com/westc/e2830febf6f2bc31ac16aa3a2cc39023)

```
YUV conversion - (ColorMatrix ?) YUV is the same as YCbCr and the matrix for that is: Y’ = 16 + ( 65.481 * R’ + 128.553 * G’ + 24.966 * B’)
Cb = 128 + (-37.797 * R’ - 74.203 * G’ + 112.0 * B’)
Cr = 128 + (112.0 * R’ - 93.786 * G’ - 18.214 * B’)
```

```
const mat3 RGBtoLMS = mat3( //Convert from color to LMS
	 17.8824,   43.5161,  4.11935,
	 3.45565,   27.1554,  3.86714,
	 0.0299566, 0.184309, 1.46709
);
const mat3 LMStoRGB = mat3( //Convert from LMS to color
	 0.0809444479,   -0.130504409,    0.116721066,
	-0.0102485335,    0.0540193266,  -0.113614708,
	-0.000365296938, -0.00412161469,  0.693511405
);
```
