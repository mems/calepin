- [Polygon Triangulation](http://www.cs.unc.edu/~dm/CODE/GEM/chapter.html)
- lightweight C program to compute 2d Voronoi diagrams and Delaunay triangulations of [Steven Fortune](http://ect.bell-labs.com/who/sjf/)
	See also
	
	- [Derek Bradley's Website](http://wayback.archive.org/web/20091212061057/http://www.derekbradley.ca/voronoi.html)
	- [Shane O Sullivans HomePage: Voronoi Resources](http://wayback.archive.org/web/20160503001512/http://www.skynet.ie/~sos/mapviewer/voronoi.php)
- VASEr is a polyline and curve renderer on OpenGL
	* [To be an Artgrammer: Drawing polylines by tessellation](http://artgrammer.blogspot.fr/2011/07/drawing-polylines-by-tessellation.html)
	* [Vase Renderer download | SourceForge.net](https://sourceforge.net/projects/vaserenderer/)
	* https://github.com/tyt2y3/vaserenderer
- [Compute the Voronoi diagram of a set of two-dimensional points](https://github.com/d3/d3-voronoi)
- Poly2Tri: Fast and Robust Simple Polygon Triangulation With/Without Holes by Sweep Line Algorithm
	- [Welcome to Poly2Tri Homepage](http://sites-final.uclouvain.be/mema/Poly2Tri/)
	- [A 2D constrained Delaunay triangulation library](https://github.com/r3mi/poly2tri.js)
	- https://github.com/greenm01/poly2tri
- [forked from: delaunay triangulation - wonderfl build flash online](http://wonderfl.net/c/nG5h)
- [Polygon Triangulation in C# - CodeProject](https://www.codeproject.com/articles/8238/polygon-triangulation-in-c)
- [IvanK Lib - fast graphics for HTML5](http://lib.ivank.net/)
- [PolyK - polygon library written in Javascript](http://polyk.ivank.net/)
- [The fastest and smallest JavaScript polygon triangulation library for your WebGL apps](https://github.com/mapbox/earcut) - This library implements a modified ear slicing algorithm
- [Triangle: A Two-Dimensional Quality Mesh Generator and Delaunay Triangulator](http://www.cs.cmu.edu/~quake/triangle.html) - Jonathan Shewchuk
- Triangle.NET - port of Jonathan Shewchuk's Triangle
	- [Triangle.NET - Home](https://triangle.codeplex.com/)
	- [Port of Triangle.NET for unity](https://github.com/parahunter/triangle-net-for-unity)
	
	See `Dynamic mesh triangulation of curved path shapes with Unity - David Wilson‏ @beepdavid.mp4`
- libtess - Polygon tesselation library of the OpenGL Utility Library (GLU)

	- [Polygon tesselation library, ported from SGI's GLU implementation to JavaScript](https://github.com/brendankenny/libtess.js)
	- [refactored version of GLU tesselator](https://github.com/memononen/libtess2)
	- [libtess2 compiled to JavaScript via emscripten](https://github.com/claus/libtess2.js)
- [OpenGL Tessellation](http://www.songho.ca/opengl/gl_tessellation.html)
- [Slice GeoJSON into vector tiles on the fly in the browser](https://github.com/mapbox/geojson-vt)
- [CS284 Lecture Page](https://people.eecs.berkeley.edu/~sequin/CS284/LECT12/LL.html) and [CS284 Lecture Page](https://people.eecs.berkeley.edu/~sequin/CS284/LECT12/L1.html) - See also next pages (nav at bottom)

To triangulate shapes (with curved paths):

1. create a polygon (Vector3 array) by sampling points along the path
2. Curves are sampled evenly by estimating the curve length first, then sampling at the required curve resolution
3. Feed polygon into triangulation algorithm to get triangle data

## Delaunay triangulation

- [Delaunay triangulation — Wikipedia](https://en.wikipedia.org/wiki/Delaunay_triangulation)
- [Triangulate: Pan Pacific Computer Conference, Beijing, China](http://paulbourke.net/papers/triangulate/)
- [mapbox/delaunator: A really fast JavaScript library for Delaunay triangulation of 2D points](https://github.com/mapbox/delaunator)
- [Bathlamos/delaunay-triangulation: A robust O(nlogn) implementation of 2D Delaunay triangulation](https://github.com/Bathlamos/delaunay-triangulation)
- [Fast Delaunay Triangulation in JavaScript](https://github.com/ironwallaby/delaunay)
- [---](http://mikolalysenko.github.io/cdt2d/) - [Constrained Delaunay Triangulation in 2D](https://github.com/mikolalysenko/cdt2d)
- [2D constrained Delaunay triangulation](https://github.com/mikolalysenko/cdt2d)
- [forked from: delaunay triangulation - wonderfl build flash online](http://wonderfl.net/c/nG5h)
- [Delaunay Triangulation](http://codepen.io/blascone/pen/AoFCx)
- https://travellermap.com/tmp/delaunay.js - Delaunay Triangulation Code, by Joshua Bell (inexorabletash)