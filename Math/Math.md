Aka geometry

See also [Algorithms](../Algorithms/Algorithms.md#resources), [Easing](../Animation/Animation.md#easing)

## Resources

- [Optimized pow() approximation for Java, C / C++, and C# – Martin Ankerl](http://martin.ankerl.com/2007/10/04/optimized-pow-approximation-for-java-and-c-c/)
- [Filling a Quadrilateral](http://loopspace.mathforge.org/HowDidIDoThat/Codea/Gradient/)
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/index.htm)
- [Math Insight Index](http://mathinsight.org/index/general)
- [Essential Math for Games Programmers](http://www.essentialmath.com/tutorial.htm)
- [Math – BetterExplained](https://betterexplained.com/articles/category/math/)
- [Javascript Math Toolkit](https://github.com/theAlgorithmist/JSMathToolkit) - math library
- [Vizutil.js is a utility library for working with basic 2D geometry.](https://noelb.github.io/vizutil.js/) - Catmull–Rom spline, near bezier, line intersection, split bezier. See https://github.com/noelb/vizutil.js
- [Table of contents — gpkit 0.5.2 documentation](http://gpkit.readthedocs.io/en/latest/) - Python package for defining and manipulating geometric programming models. see https://github.com/hoburg/gpkit
- [GraphFree Home](http://www.graphfree.com/)
- ![ALEFReferenceCards Trigonometry   Side 1](ALEFReferenceCards-Trigonometry%20-%20Side%201.Jpg)
- ![ALEFReferenceCards Trigonometry   Side 2](ALEFReferenceCards-Trigonometry%20-%20Side%202.Jpg)

## Imaginary Number

Aka `i`

![Imaginary Example2 BetterExplained](imaginary_example2%20BetterExplained.png)

- [A Visual, Intuitive Guide to Imaginary Numbers – BetterExplained](https://betterexplained.com/articles/a-visual-intuitive-guide-to-imaginary-numbers/)

## Arc-tangent

```as3
/**
 * Computes and returns the angle of the point <code>y/x</code> in radians, when measured counterclockwise
 * from a circle's <em>x</em> axis (where 0,0 represents the center of the circle).
 * The return value is between positive pi and negative pi.
 *
 * @author Eugene Zatepyakin
 * @author Joa Ebert
 * @author Patrick Le Clec'h
 *
 * @param y A number specifying the <em>y</em> coordinate of the point.
 * @param x A number specifying the <em>x</em> coordinate of the point.
 *
 * @return A number.
 */
public static function atan2(y:Number, x:Number):Number {
	var sign:Number = 1.0 - (int(y < 0.0) << 1)
	var absYandR:Number = y * sign + 2.220446049250313e-16
	var partSignX:Number = (int(x < 0.0) << 1) // [0.0/2.0]
	var signX:Number = 1.0 - partSignX // [1.0/-1.0]
	absYandR = (x - signX * absYandR) / (signX * x + absYandR)
	return ((partSignX + 1.0) * 0.7853981634 + (0.1821 * absYandR * absYandR - 0.9675) * absYandR) * sign
}
```

- [Code Twiddling – atan2 , tricks !!! **updated**](http://guihaire.com/code/?p=1168) - compare performance and accurency of differents implementation with AS3

## Geometry

- [Geometry, Surfaces, Curves, Polyhedra](http://paulbourke.net/geometry/) - resources for "Intersection of a Line and a Sphere (or circle)", "Intersection of two spheres", "Distributing Points on a Sphere", etc.

## Matrix

- [Matrices in Codea](http://loopspace.mathforge.org/HowDidIDoThat/Codea/Matrices/)
- [Matrix Multiplication](http://matrixmultiplication.xyz/)
- [A Programmer’s Intuition for Matrix Multiplication – BetterExplained](https://betterexplained.com/articles/matrix-multiplication/)
- [CleVR Actionscript 3 Library](https://github.com/ascorbic/clevrlib) - This library provides some classes for linear algebra. It's ported from the NIST's JAMA Java Matrix library
- [JAMA: Java Matrix Package](http://math.nist.gov/javanumerics/jama/) - 

## Pythagorean Theorem

- [My Favourite Proof](http://loopspace.mathforge.org/CountingOnMyFingers/FavouriteProof/)
- [Pythagorean Theorem and its many proofs](http://www.cut-the-knot.org/pythagoras/)

## Trigonometric

- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/sincos/sincos.htm) - a sin/cos trick

## 3D

- [Spherical Coordinates -- from Wolfram MathWorld](http://mathworld.wolfram.com/SphericalCoordinates.html)

### Sphere

- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/spherefunctions/spherefunctions.htm) - sphere functions
- [on ray-sphere | el trastero](http://www.iquilezles.org/blog/?p=2411) - Sphere Intersection

### 3D orientation

- [deviceorientation - quaternion & rotation matrix manipulation - w/ three.js](http://rawgit.com/richtr/threeVR/master/examples/vr_basic.html) - see [An orientation-aware Virtual Reality controller for web browsers built on top of three.js](https://github.com/richtr/threeVR/)
- [FULLTILT DeviceOrientation three.js test page](http://rawgit.com/adtile/Full-Tilt/master/examples/vr_test.html) - see https://github.com/adtile/Full-Tilt

## Circle outer tangent

Circle outer tangent of 2 circles

```js
// From https://github.com/bit101/lab/blob/master/dailies/170318.js
function circleTangents(c0, c1) {
	// probably not the most efficient algorithm possible.
	// but it works and I understand it.
	var h = bitlib.math.dist(c0, c1),	// hypotenuse of triangle
		adj = c0.r - c1.r,				// adjacent side of triangle
		a0 = Math.atan2(c1.y - c0.y,
		                c1.x - c0.x),	// angle between circles
		a1 = Math.acos(adj / h),		// angle of triangle
		a2 = a0 - a1,					// angle to one tangent point
		a3 = a0 + a1,					// angle to other tangent point
		p0 = {							// x, y of one tangent point
			x: c0.x + Math.cos(a2) * c0.r,
			y: c0.y + Math.sin(a2) * c0.r
		},
		p1 = {							// x, y of other tangent point
			x: c0.x + Math.cos(a3) * c0.r,
			y: c0.y + Math.sin(a3) * c0.r
		};
	// swap everything to the other circle's viewpoint and repeat.
	a0 += Math.PI;
	a1 = Math.acos(-adj / h);
	a2 = a0 - a1;
	a3 = a0 + a1;
	var p2 = {
			x: c1.x + Math.cos(a2) * c1.r,
			y: c1.y + Math.sin(a2) * c1.r
		},
		p3 = {
			x: c1.x + Math.cos(a3) * c1.r,
			y: c1.y + Math.sin(a3) * c1.r
		};
	return [p0, p1, p2, p3];
}
```

- [170318](https://bit101.github.io/lab/dailies/170318.html) - [lab/170318.js at master · bit101/lab](https://github.com/bit101/lab/blob/master/dailies/170318.js)
- [Tangent lines to circles — Wikipedia](https://en.wikipedia.org/wiki/Tangent_lines_to_circles#Outer_tangent)

## Linear Interpolation

Aka lerp, mix

```js
/**
 * @example
 * lerp(0, 100, 0.5); // 50
 * lerp(20, 80, 0); // 20
 * lerp(30, 5, 1); // 5
 * lerp(-1, 1, 0.5); // 0
 * lerp(0.5, 1, 0.5); // 0.75
*/
function lerp (start, end, t) {
	return start * (1 - t) + end * t;
}
```

- [Linear interpolation - Wikipedia](https://en.wikipedia.org/wiki/Linear_interpolation)

## Percentage

> X% of Y = Y% of X
> 27% of 73 is the same as 73% of 27
