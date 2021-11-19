Aka curve, bézier

See also [Rendering text](Graphics#rendering-text)

> Catmull–Rom splines are frequently used to get smooth interpolated motion between key frames. For example, most camera path animations generated from discrete key-frames are handled using Catmull–Rom splines

## Resources

- [Cubic Hermite spline — Wikipedia](https://en.wikipedia.org/wiki/Cubic_Hermite_spline)
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/minispline/minispline.htm) - minimal code for splines
- [Spline Interpolation](http://scaledinnovation.com/analytics/splines/splines.html) and [About Spline Interpolation](http://scaledinnovation.com/analytics/splines/aboutSplines.html)
- [Vizutil.js is a utility library for working with basic 2D geometry.](https://noelb.github.io/vizutil.js/) - Catmull–Rom spline. See https://github.com/noelb/vizutil.js
- [Centripetal Catmull–Rom spline — Wikipedia](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline)

## Rasterization

See [bézier rasterization](#bézier-rasterization)

## Bézier

A bezier spline is an aggregation of bezier curves (could be have different polynomial: cubic, quadratic or n) ([polybezier](https://en.wikipedia.org/wiki/Composite_B%C3%A9zier_curve))

See also [Reduce points - Polyline simplification](Reduce points - Polyline simplification)

- (see comments) [blog.rails2u.com » Blog Archive » Accurate bezier special property for Tweener](http://wayback.archive.org/web/20080518175320/http://blog.rails2u.com/2007/10/03/accurate-bezier-special-property-for-tweener/)

```js
const anchor1 = {x: 0, y: 0};
const anchor2 = {x: 100, y: 0};
const control1 = {x: 0, y: -100};
const control2 = {x: 100, y: -100};
const position = 0.5; // between 0 and 1

const posX = Math.pow(position, 3) * (anchor2.x + 3 * (control1.x - control2.x) - anchor1.x)
	+ 3 * Math.pow(positie, 2) * (anchor1.x - 2 * control1.x + control2.x)
	+ 3 * position * (control1.x - anchor1.x) + anchor1.x;

const posY = Math.pow(position, 3) * (anchor2.y + 3 * (control1.y - control2.y) - anchor1.y)
	+ 3 * Math.pow(position, 2) * (anchor1.y - 2 * control1.y + control2.y)
	+ 3 * position * (control1.y - anchor1.y) + anchor1.y;
```

```
// given points p0, p0Out, and p1In, and p1, and t varying from 0.0 to 1.0...
a0 = (1 - t) ** 3
a1 = 3 * (1 - t) ** 2 * t
a2 = 3 * (1 - t) * t ** 2
a3 = t ** 3

// calculate x and y
x = a0 * p0.x + a1 * p0.xOut + a2 * p1.xIn + a3 * p1.x
y = a0 * p0.y + a1 * p0.yOut + a2 * p1.yIn + a3 * p1.y
```

Curves (Bezier)

- [The Beauty of Bézier Curves - YouTube](https://www.youtube.com/watch?v=aVwxzDHniEw)
- [A Primer on Bézier Curves](https://pomax.github.io/bezierinfo/) and https://github.com/pomax/BezierInfo-2
- [Approximating Cubic Bezier Curves in Flash MX](http://timotheegroleau.com/Flash/articles/cubic_bezier_in_flash.htm)
- [Bezier Curves: The Math](http://www.moshplant.com/direct-or/bezier/math.html)
- [Guru's Lair: Cubic Spline & Bezier Curves Library](http://www.tinaja.com/cubic01.shtml)
- [Algorithme de Casteljau — Wikipédia](https://fr.wikipedia.org/wiki/Algorithme_de_Casteljau)
- [Bézier curve - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/B%C3%A9zier_curve)
- bezierjs [Bezier.js, for doing Bezier curve things](http://pomax.github.io/bezierjs/)
- [Bézier Curves by Gernot Hoffmann](https://seant23.files.wordpress.com/2010/11/beziercurvespostscript.pdf)
- [Exploring Bezier Curves](https://richardfuhr.neocities.org/BusyBCurves.html)
- [Solving Quadratics with a Ruler and Compass](http://loopspace.mathforge.org/CountingOnMyFingers/QuadraticCompass/)
- [graphics - bezier path widening - Stack Overflow](https://stackoverflow.com/questions/3205819/bezier-path-widening)
- [Drawing Bézier Curves – Bartosz Ciechanowski](https://web.archive.org/web/20201112015848/https://ciechanow.ski/drawing-bezier-curves/)
- [Drawing a cubic bezier curve using actionscript 3 | Paul Tondeur](http://wayback.archive.org/web/20160712042256/http://blog.paultondeur.com/2008/03/09/drawing-a-cubic-bezier-curve-using-actionscript-3)
- [Constant speed following bezier curve - math & physics - Devmaster Forum](http://forum.devmaster.net/t/constant-speed-following-bezier-curve/7963) and [Spin-X Engine Community - Constant Speed Cubic Spline Interpolation](http://wayback.archive.org/web/20130805215911/http://community.spinxengine.com/content/19-constant-speed-cubic-spline-interpolation.html)
- [Bézier Path Algorithms | Dev.Mag](http://devmag.org.za/2011/06/23/bzier-path-algorithms/)
- [Bézier Curves for your Games: A Tutorial | Dev.Mag](http://devmag.org.za/2011/04/05/bzier-curves-a-tutorial/)
- [Computer Aided Geometric Design](http://tom.cs.byu.edu/~557/text/cagd.pdf) - mathematical description of shape for use in computer graphics. Vector algebra, equations for lines and conic sections, homogeneous coordinates, etc.
- _Curves and Surfaces for Computer Graphics_ by David Salomon
- [Beziers (our approach…!) « miaumiau interactive studio](http://www.miaumiau.cat/2010/03/beziers-our-approach/)
- [math - How to draw Cubic Bezier in WebGL/OpenGL - Stack Overflow](https://stackoverflow.com/questions/35534562/how-to-draw-cubic-bezier-in-webgl-opengl)
- [MDK : Curvy blues](http://www.mdk.org.pl/2007/10/27/curvy-blues) - See [fragment shader](cubic-shader.pso) and [shader implementation](quadratic-shader.pso)
- [Flex and ActionScript Development Tips: Drawing Dashed Lines, Arcs, and Cubic Curves](http://flexdevtips.blogspot.fr/2010/01/drawing-dashed-lines-and-cubic-curves.html) [GraphicsUtils](GraphicsUtils.as)
- [Rendering SVG Paths in WebGL | CSS-Tricks](https://css-tricks.com/rendering-svg-paths-in-webgl/)
- [Resolution independent rendering of Bezier curves in WebGL](https://gist.github.com/claus/1396250) [Resolution independent rendering of Bezier curves in WebGL](Resolution independent rendering of Bezier curves in WebGL.html)
- [Anti-Grain Geometry - Adaptive Subdivision of Bezier Curves](http://antigrain.com/research/adaptive_bezier/)
- [WebGL SWF shape renderer](http://codeazur.com.br/shumway/gl_tiger/)
- [MDK : Vector drawing: OpenGL shaders and cairo](http://mdk.org.pl/2007/8/6/vector-drawing-opengl-shaders-and-cairo)
- [C++ Programming](https://nccastaff.bournemouth.ac.uk/jmacey/RobTheBloke/www/opengl_programming.html#3)
- [Bézier Curves and Surfaces: the Utah Teapot (Bézier Curve)](http://www.scratchapixel.com/lessons/advanced-rendering/bezier-curve-rendering-utah-teapot)
- [Drawing a cubic bezier curve using actionscript 3 | Paul Tondeur](http://wayback.archive.org/web/20160712042256/http://blog.paultondeur.com/2008/03/09/drawing-a-cubic-bezier-curve-using-actionscript-3)
- [Bezier curve helper functions for JavaScript](https://github.com/jsplumb/jsBezier)
- [Cubic-to-quadratic bezier curve conversion](https://github.com/googlei18n/cu2qu) - converts any cubic curves to quadratic
- [Bitmap/Bézier curves/Cubic - Rosetta Code](http://rosettacode.org/wiki/Bitmap/B%C3%A9zier_curves/Cubic)
- [Bitmap/Bézier curves/Quadratic - Rosetta Code](http://rosettacode.org/wiki/Bitmap/B%C3%A9zier_curves/Quadratic)

Bezier 3D

- [Bezier Surface](http://paulbourke.net/geometry/bezier/)
- [Spline Surface](http://paulbourke.net/geometry/spline/)
- [Simple Surface Editor « miaumiau interactive studio](http://www.miaumiau.cat/2010/03/simple-surface-editor/)

- [Parametric Cubic Curves](http://spec.winprog.org/curves/)

See also [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/fourier/fourier.htm) - fourier series for key frame interpolation

### Bézier rasterization

- [GPU Gems 3 - Chapter 25. Rendering Vector Art on the GPU](http://http.developer.nvidia.com/GPUGems3/gpugems3_ch25.html) - See also [Resolution independent cubic bezier drawing on GPU (Blinn/Loop) - Stack Overflow](https://stackoverflow.com/questions/15519142/resolution-independent-cubic-bezier-drawing-on-gpu-blinn-loop/31128364#31128364)
- [Path Rasterizer for OpenVG](https://brage.bibsys.no/xmlui/handle/11250/252871) - See [Path Rasterizer for OpenVG](Path Rasterizer for OpenVG.pdf). See also [OpenVG - The Standard for Vector Graphics Acceleration](https://www.khronos.org/openvg/)
- [NVIDIA GPU-accelerated Path Rendering - SVG Part 1 - YouTube](https://www.youtube.com/watch?v=bCrohG6PJQE) (3 videos) and [NV_path_rendering Introduction (Part 1) - YouTube](https://www.youtube.com/watch?v=0IDyZof2pRI) (4 videos) - `NV_path_rendering` OpenGL extension to GPU-accelerate path rendering. See [NV Path Rendering | NVIDIA Developer](https://developer.nvidia.com/nv-path-rendering) and [NV Path Rendering Videos | NVIDIA Developer](https://developer.nvidia.com/nv-path-rendering-videos)
- [Resolution independent rendering of Bezier curves in WebGL](https://gist.github.com/claus/1396250)

Based on "Resolution Independent Curve Rendering using Programmable Graphics Hardware", paper and implementations:

- [Resolution Independent Curve Rendering using Programmable Graphics Hardware](http://research.microsoft.com/en-us/um/people/cloop/loopblinn05.pdf) - The paper. See [Resolution Independent Curve Rendering using Programmable Graphics Hardware - Microsoft Research](https://www.microsoft.com/en-us/research/publication/resolution-independent-curve-rendering-using-programmable-graphics-hardware/)
- [Bézier curve rendered via OpenGL fragment-shader - YouTube](https://www.youtube.com/watch?v=K5u8ZZBWSdw) - See https://launchpad.net/gl-fragment-curves
- [Test: GPU Quadratic Curve Rendering « Rubén Penalva's Blog](http://www.rpenalva.com/blog/?p=107#more-107)
- [Loop-Blinn TTF rendering](https://cscheid.github.io/lux/demos/loopblinn/loopblinn.html) - Quickly draw resolution-independent, pixel-accurate text with very few polygons. See https://github.com/cscheid/lux/tree/master/demos/loopblinn

### Compute length of bézier

Length of bezier cubic

> > It's surprisingly easy. An approximate length of a 3D cubic Bezier curve is the average of its chord length and the sum of the lengths of its control net sides. This approximated average converges on the true arc length very quickly as the parametric domain is reduced.
> >
> > In English: the chord length is the length of the line segment between the arc endpoints. The control net is the three line segments that define the cubic Bezier. The sum of the lengths of those three line segments, added to the chord length, and divided by two, gives a good approximation to true cubic Bezier arc length.
> >
> > To get a better approximation, split the cubic Bezier into several smaller cubic Beziers, and perform the operation I described above on each of them, and sum their lengths for the arc length of the entire cubic Bezier.
> — [3D Cubic Bezier Segment Length](https://www.opengl.org/discussion_boards/showthread.php/172373-3D-Cubic-Bezier-Segment-Length?p=1209064&viewfull=1#post1209064)
>
> 	Bezier bezier = Bezier (p0, p1, p2, p3);
>
> 	chord = (p3-p0).Length;
> 	cont_net = (p0 - p1).Length + (p2 - p1).Length + (p3 - p2).Length;
>
> 	app_arc_length = (cont_net + chord) / 2;
— [c - Cheap way of calculating cubic bezier length - Stack Overflow](https://stackoverflow.com/questions/29438398/cheap-way-of-calculating-cubic-bezier-length/37862545#37862545)


- [Arc length — Wikipedia](https://en.wikipedia.org/wiki/Arc_length)
- Arc length [A Primer on Bézier Curves](https://pomax.github.io/bezierinfo/#arclength)
- [Arc Length of Bézier Curves - Mathematics Stack Exchange](http://math.stackexchange.com/questions/12186/arc-length-of-b%C3%A9zier-curves)
- [c - Cheap way of calculating cubic bezier length - Stack Overflow](https://stackoverflow.com/questions/29438398/cheap-way-of-calculating-cubic-bezier-length)
- [CG Notes: Arc Length of Cubic Bezier Curves](http://steve.hollasch.net/cgindex/curves/cbezarclen.html) - see also [javascript - Trying to find length of a bezier curve with 4 points - Stack Overflow](https://stackoverflow.com/questions/17099776/trying-to-find-length-of-a-bezier-curve-with-4-points)
- [A More Efficient Way of Calculating the Length of a Bezier Curve. Part II – Carlos M. Icaza](http://www.carlosicaza.com/2012/08/12/an-more-efficient-way-of-calculating-the-length-of-a-bezier-curve-part-ii/)
- [Length of a Generalized Quadratic Bezier Curve in 3d - Math and Physics - GameDev.net](https://www.gamedev.net/topic/551455-length-of-a-generalized-quadratic-bezier-curve-in-3d/)
- [Calculating the length of a Bezier curve... - Math and Physics - GameDev.net](https://www.gamedev.net/topic/313018-calculating-the-length-of-a-bezier-curve/)
- [Fast cubic Bezier curve length calculation library](https://github.com/HTD/FastBezier) - Test of line interpolation, midpoint quadratic interpolation and adaptive quadratic interpolation
- [Quadratic Bezier curve length](http://www.malczak.linuxpl.com/blog/quadratic-bezier-curve-length/)
- [Approximate length of a cubic bezier curve](https://www.lemoda.net/maths/bezier-length/index.html)
- [Finding the length of a cubic Bezier curve? : math](https://www.reddit.com/r/math/comments/30osst/finding_the_length_of_a_cubic_bezier_curve/)

### Points distribution on bézier

For segmentation, dashes, text on curve or motion keyframes

> Distributing points on a Bezier curve is challenging. The curve is created with a t value that goes from 0 to 1. Using that for distribution of points gives you areas of wide spacing, and other areas of high density points.
> One solution is to convert the path into a bunch of very small, roughly equal sized line segments and use those for the distribution. It's an approximation, but much improved.
— Keith Peters (aka bit101) [17/02/26](https://bit101.github.io/lab/dailies/170226.html)

- [javascript - Dashed Curves on Html5 Canvas Bezier - Stack Overflow](https://stackoverflow.com/questions/7352769/dashed-curves-on-html5-canvas-bezier)
- [javascript - dotted stroke in \<canvas\> - Stack Overflow](https://stackoverflow.com/questions/4576724/dotted-stroke-in-canvas)
- [17/02/26](https://bit101.github.io/lab/dailies/170226.html) and [170227](https://bit101.github.io/lab/dailies/170227.html) - Use the "Segmentize" checkbox. See https://github.com/bit101/lab/blob/master/dailies/170226.js and https://github.com/bit101/lab/blob/master/dailies/170227.js

Path like car on road or train on trailroad / rail tracks

- Lot of infos [Curved Paths](http://www.redblobgames.com/articles/curved-paths/), [Road Building Applet](http://theory.stanford.edu/~amitp/game-programming/road-applet/roads.html) and [Blobs in Games: Road building applet](http://simblob.blogspot.fr/2004/10/road-building-applet.html)
- [The Starting Point for a Train Game with Freeform Tracks | Learn & Master Cocos2D Game Development](http://www.learn-cocos2d.com/2012/07/starting-point-train-game-freeform-tracks/) https://github.com/LearnCocos2D/LearnCocos2D/tree/master/RailCarDrivingOnTrackTest
- [mathematics - What are some methods to represent train tracks? - Game Development Stack Exchange](http://gamedev.stackexchange.com/questions/504/what-are-some-methods-to-represent-train-tracks)
- [Transportation - Realistic Highway Mod (RHM2) | XLNation - Cities XXL](http://xlnation.city/resources/realistic-highway-mod-rhm2.371/) `XL_Nation_Pitty_RHM2.rar` (auto extra archive/exe in RAR) with data saved as [MCPK](https://sourceforge.net/projects/mcpkutil/) (rename files as *.pak)

### Offset a bézier

- [Offset Bézier Curves | All I'm Saying Is...](https://seant23.wordpress.com/2010/11/12/offset-bezier-curves/)
- see `.offset(d) and .offset(t, d)` and `.outline(d), .outline(d1,d2), and .outline(d1,d2,d3,d4)` [Bezier.js, for doing Bezier curve things](http://pomax.github.io/bezierjs/)
- [An offset algorithm for polyline curves](https://seant23.files.wordpress.com/2010/11/anoffsetalgorithm.pdf)
- [Fast, precise flattening of cubic Bézier path and offset curves](https://seant23.files.wordpress.com/2010/11/fastpreciseflatteningofbeziercurve.pdf)

### Bézier surface

Aka bézier patch, bézier plane

2D or 3D
![Tws](Bézier%20surface/tws.gif)
![Bezier Surface](bezier-surface.gif)

- [Curves and Surfaces – Bartosz Ciechanowski](https://web.archive.org/web/20211111051947/https://ciechanow.ski/curves-and-surfaces/)
- [Bézier surface — Wikipedia](https://en.wikipedia.org/wiki/B%C3%A9zier_surface)
- [CS184 Spline Guest lecture #1](https://web.archive.org/web/20170307093802/https://people.eecs.berkeley.edu/~sequin/CS184/GuestLecture_05/SplineLect1.html) and [CS184 Spline Guest lecture #2](https://web.archive.org/web/20170307093801/https://people.eecs.berkeley.edu/~sequin/CS184/GuestLecture_05/SplineLect2.html)
- [Envelope Distort with ActionScript | Neuro Productions](http://wayback.archive.org/web/20160322114832/http://www.neuroproductions.be/experiments/envelope-distort-with-actionscript/)
