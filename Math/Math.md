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
- [BiVector.net: Geometric Algebra Resources](https://bivector.net/)

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

## Pythagorean Theorem

- [My Favourite Proof](http://loopspace.mathforge.org/CountingOnMyFingers/FavouriteProof/)
- [Pythagorean Theorem and its many proofs](http://www.cut-the-knot.org/pythagoras/)

## Trigonometric

Aka sine, cosine, tangent

- [Trigonometric functions - Wikipedia](https://en.wikipedia.org/wiki/Trigonometric_functions)
- [Inigo Quilez :: fractals, computer graphics, mathematics, shaders, demoscene and more](https://web.archive.org/web/20200915070946/https://www.iquilezles.org/www/articles/sincos/sincos.htm) - a sin/cos trick
- [How does C compute sin() and other math functions? - Stack Overflow](https://stackoverflow.com/questions/2284860/how-does-c-compute-sin-and-other-math-functions)
- [LucasVB (1ucasvb) on Twitter: "Here's all the trigonometric functions in a way things actually make sense all around the circle. All the main identities are obvious in this geometric interpretation. https://t.co/2CT0YcFa0Q" / Twitter](https://twitter.com/LucasVB/status/1378529237322334208)
- [ZX Sine | Arkeoblog](https://web.archive.org/web/20210918105239/https://albertveli.wordpress.com/2015/01/10/zx-sine/) - Compute `sin()` and `cos()` using Chebyshev polynomials
- [Arduino/AVR and ZX Spectrum: sin() routines. – Niels Moseley's bloggy bits](https://web.archive.org/web/20211007150920/https://namoseley.wordpress.com/2012/09/26/arduinoavr-and-zx-spectrum-sin-routines/)

Taylor series:

```
// AVR C lib
C0 = 1.0000000000;
C1 = -0.1666666664;
C2 = 0.0083333315;
C3 = -0.0001984090;
C4 = 0.0000027526;
C5 = -0.0000000239;

P(x) = c_0\cdot x + c_1\cdot x^3 + c_2\cdot x^5 + c_3\cdot x^7 + c_4\cdot x^9 + c_5\cdot x^{11}.
```

[Z80 / ZX Spectrum version](https://web.archive.org/web/20210918105239/https://albertveli.wordpress.com/2015/01/10/zx-sine/):

```
#define T0(x) ( 1 )
#define T1(x) ( x )
#define T2(x) ( 2 * x*x - 1 )
#define T3(x) ( 4 * x*x*x - 3 * x )
#define T4(x) ( 8 * x*x*x*x - 8 * x*x + 1 )
#define T5(x) ( 16 * x*x*x*x*x - 20 * x*x*x + 5 * x )

#define C0 1.276278962f
#define C1 -.285261569f
#define C2 0.009118016f
#define C3 -.000136587f
#define C4 0.000001185f
#define C5 -.000000007f

#define P(z) ( C0 * T0(z) + C1 * T1(z) + C2 * T2(z) + C3 * T3(z) + C4 * T4(z) + C5 * T5(z) )

float zx_sin(float x)
{
   double w = 4 * x;
   double z = 2 * w * w - 1;

   return P(z) * w;
}

/*
Coefficients for cos:
#define C0 0.472001216
#define C1 -0.499403258
#define C2 0.027992080
#define C3 -0.000596695
#define C4 0.000006704
#define C5 -0.000000047

Coefficients for arctan, arcsin, arceos, e^x, e^-x, log(1+x) see https://web.archive.org/web/20210918105351/http://www.ams.org/journals/mcom/1954-08-047/S0025-5718-1954-0063487-2/S0025-5718-1954-0063487-2.pdf
*/
```

## Matrix

- [Matrices in Codea](http://loopspace.mathforge.org/HowDidIDoThat/Codea/Matrices/)
- [Matrix Multiplication](http://matrixmultiplication.xyz/)
- [A Programmer’s Intuition for Matrix Multiplication – BetterExplained](https://betterexplained.com/articles/matrix-multiplication/)
- [CleVR Actionscript 3 Library](https://github.com/ascorbic/clevrlib) - This library provides some classes for linear algebra. It's ported from the NIST's JAMA Java Matrix library
- [JAMA: Java Matrix Package](http://math.nist.gov/javanumerics/jama/) -

## 3D

- [Spherical Coordinates -- from Wolfram MathWorld](http://mathworld.wolfram.com/SphericalCoordinates.html)

### Sphere

- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/spherefunctions/spherefunctions.htm) - sphere functions
- [on ray-sphere | el trastero](http://www.iquilezles.org/blog/?p=2411) - Sphere Intersection
- [How to evenly distribute points on a sphere more effectively than the canonical Fibonacci Lattice | Extreme Learning](https://web.archive.org/web/20210901181405/http://extremelearning.com.au/how-to-evenly-distribute-points-on-a-sphere-more-effectively-than-the-canonical-fibonacci-lattice/)
- [Random Position On The Surface Of A Sphere | David Lochhead](https://web.archive.org/web/20210908081512/https://blog.davidlochhead.xyz/posts/2017-10-12-random-position-on-the-surface-of-a-sphere.html#first-try-%E2%80%94-random-vector-with-setlength)

### 3D orientation

- [deviceorientation - quaternion & rotation matrix manipulation - w/ three.js](http://rawgit.com/richtr/threeVR/master/examples/vr_basic.html) - see [An orientation-aware Virtual Reality controller for web browsers built on top of three.js](https://github.com/richtr/threeVR/)
- [FULLTILT DeviceOrientation three.js test page](http://rawgit.com/adtile/Full-Tilt/master/examples/vr_test.html) - see https://github.com/adtile/Full-Tilt

### Traveling Salesman Problem

- [DiegoVicen/som-tsp: Solving the Traveling Salesman Problem using Self-Organizing Maps](https://github.com/DiegoVicen/som-tsp)
- [Using Self-Organizing Maps to solve the Traveling Salesman Problem](https://web.archive.org/web/20210906072152/https://diego.codes/post/som-tsp/)
- [(2) Matt Dzugan on Twitter: "📣 Fun Puzzle: How can we take advantage of the widely researched “Traveling-Salesman-Problem” tools and algorithms to solve a related “Single-Pickup, Multi-Dropoff” problem? spoiler (and code) in thread🧵 https://t.co/PuEOM9ORHf" / Twitter](https://twitter.com/MattDzugan/status/1438927293661995012)
- [Solving Single-Pickup Multi-Dropoff as Traveling Salesman Problem / Matt Dzugan / Observable](https://observablehq.com/@mattdzugan/solving-single-pickup-multi-dropoff-as-traveling-salesman)

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
