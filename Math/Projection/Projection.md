Aka map projection and rotation

- [Lens Correction / Distortion](http://paulbourke.net/miscellaneous/lenscorrection/)
- [Quadrilateral demo - Cassowary Javascript](http://www.badros.com/greg/cassowary/js/quaddemo.html)
- [Nonlinear Projections](http://scaledinnovation.com/analytics/nonlinear/fisheye.html)
- [The Perspective and Orthographic Projection Matrix (What Are Projection Matrices and Where/Why Are They Used?)](http://wayback.archive.org/web/20161029031955/http://scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix)
- [Computer Graphics and Multimedia](https://www.graphics.rwth-aachen.de/software/image-localization) - Estimating the position and orientation of a camera from an image by finding correspondences between structures seen in the image and a 3D representation of the scene
- [Oblique projection — Wikipedia](https://en.wikipedia.org/wiki/Oblique_projection)
- [Isometric projection — Wikipedia](https://en.wikipedia.org/wiki/Isometric_projection)
- [Miscellaneous Transformations and Projections](http://paulbourke.net/geometry/transformationprojection/)
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/sphereproj/sphereproj.htm) - sphere projection
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/sphereocc/sphereocc.htm) - sphere visibility
- [Raster map projection with ActionScript 3 | Andy Woodruff](http://andywoodruff.com/blog/raster-map-projection-with-actionscript-3/)
- [proj.4 — proj.4 4.9.3 documentation](http://proj4.org/) and [proj4j](https://github.com/Proj4J/proj4j) (Java port) - library to transform point coordinates from one geographic coordinate system to another
- [D3.js - Data-Driven Documents](https://d3js.org/) - See https://github.com/d3/d3-geo and https://github.com/d3/d3-geo-projection
- [Two points perspective](http://codepen.io/ge1doot/pen/dvMXOM)

Note: [resample](Resample) could be required to fix pixels

Simple 3D projection to 2D plan:

	scale2D = f / (f + z);//f = field of view
	x2D = x * scale2D;
	y2D = y * scale2D;

Where `x`, `y` and `z` are position in 3D space, and `x2D` and `y2D` are the position in 2D plan.

	T = focalLength/(focalLength + z)

	fov = 2.0 * Math.atan( (width - 1) / (2 * focalX) );
	nearPlane = focalX / 32;
	farPlane = focalX * 32;

## Homography

Aka Deprojection, extract plane from projection

- [Fast texture extraction - wonderfl build flash online](http://wonderfl.net/c/vbla) - see [Inverse homography using drawTriangles() | Coding on acid.](https://makc3d.wordpress.com/2010/10/21/inverse-homography-drawtriangles/)
- [\[image\] géométrie projective (homography)](https://www.developpez.net/forums/d740403/general-developpement/algorithme-mathematiques/contribuez/image-geometrie-projective-homography/)
- [Saqoosha :: スーパー高速に射影変換するには](https://saqoo.sh/a/1750)
- [Homography — Wikipedia](https://en.wikipedia.org/wiki/Homography)
- [Homography « HIDIHO!](http://www.barradeau.com/hidiho/index1098.html?p=59) - [DistortImage 2.0, la façon la plus performante de déformer des images en Actionscript](http://wayback.archive.org/web/20090506015557/http://kiroukou.media-box.net:80/blog/mes-recherches-sur-flash/64-distortimage-20-la-facon-la-plus-performante-de-deformer-des-images-en-actionscript.html) and wayback.archive.org/web/20090506015557/http://kiroukou.media-box.net/blog/wp-content/uploads/2006/03/Distort.zip

## Inverse homography

Aka compute projection from points, distort image, corners to matrix (3D), from 2D points to (projected) 3D plan

- [The best drawPlane/distortImage method, ever – Zeh Fernando](http://zehfernando.com/2010/the-best-drawplane-distortimage-method-ever/)
- [corners to Matrix3D - wonderfl build flash online](http://wonderfl.net/c/sxQJ)
- [Interactive perspective-distorted sprites – Zeh Fernando](http://zehfernando.com/2011/interactive-perspective-distorted-sprites/) - a better solution
- https://github.com/zeh/as3/blob/19424a4abd3701c18e6bb9f7261840ce2400cacc/com/zehfernando/display/abstracts/PerspectiveSprite.as
- [ProjectionMapping](http://cake23.de/projectionMapping/) 

## Depth sorting

Aka z-sorting, depth buffer

- [Z-buffering — Wikipedia](https://en.wikipedia.org/wiki/Z-buffering)
- [Painter's algorithm — Wikipedia](https://en.wikipedia.org/wiki/Painter's_algorithm)

## Orthographic projection

- [Orthographic projection — Wikipedia](https://en.wikipedia.org/wiki/Orthographic_projection)

## Sphere to 2D

Earth map

- [The problem with maps.](http://mjmdavis.com/showing/2017/05/16/The-problem-with-maps.html)
- [A Gallery of Map Projections](http://www.csiss.org/map-projections/index.html)
- [Map Projections -- from Wolfram MathWorld](http://mathworld.wolfram.com/topics/MapProjections.html)
- [WorldWide Telescope Projection Reference](http://www.worldwidetelescope.org/docs/worldwidetelescopeprojectionreference.html)
- [Maps](https://www.jasondavies.com/maps/) - projection and geometric computation about maps using D3.js
- [Map Projections: Interrupted Maps](http://www.progonos.com/furuti/MapProj/Normal/ProjInt/projInt.html)
- [Microsoft Word - dmswart sebprzd Bridges 2013.doc - bridges2013-217.pdf](http://archive.bridgesmathart.org/2013/bridges2013-217.pdf)