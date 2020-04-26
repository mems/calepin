## Noise

- [Perlin noise — Wikipedia](https://en.wikipedia.org/wiki/Perlin_noise)
- [Value noise — Wikipedia](https://en.wikipedia.org/wiki/Value_noise)
- [Gradient noise — Wikipedia](https://en.wikipedia.org/wiki/Gradient_noise)
- [The problem with 3D blue noise | Moments in Graphics](http://momentsingraphics.de/?p=148)
- [A SciPy implementation of the void-and-cluster method for generation of blue noise textures with arbitrary dimension](https://github.com/MomentsInGraphics/BlueNoise)
- [Improved Noise reference implementation](http://mrl.nyu.edu/~perlin/noise/)
- [Perlin Noise](http://wayback.archive.org/web/20160510013854/http://freespace.virgin.net/hugo.elias/models/m_perlin.htm)
- [Value Noise and Procedural Patterns: Part 1 (Introduction)](http://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/procedural-patterns-noise-part-1)
- [Perlin Noise: Part 2 (Perlin Noise)](http://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/perlin-noise-part-2)
- [Quasimondo - Mario Klingemann's Flash Blog: Optimizing Perlin Noise](http://www.quasimondo.com/archives/000672.php) - see http://www.quasimondo.com/examples/OptimizedPerlin.as
- [The Perlin noise math FAQ](https://mzucker.github.io/html/perlin-noise-math-faq.html)
- [advanced perlin noise - Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/morenoise/morenoise.htm)
- [Making noise by Ken Perlin](http://web.archive.org/web/20160422091821/http://www.noisemachine.com/talk1/)
- [Free blue noise textures | Moments in Graphics](http://momentsingraphics.de/?p=127)
- [implementation - How is Perlin-noise in flash implemented? - Stack Overflow](https://stackoverflow.com/questions/8467685/how-is-perlin-noise-in-flash-implemented) - "Flash implementation is [...] based on integer calculations rather than floats. This would explain why the rendering is fast"
- [Humus - 3D](http://www.humus.name/index.php?page=3D&ID=29) - Perlin noise in a fragment program
- [Noise-Based Particles, Part I at The Little Grasshopper](http://prideout.net/blog/?p=63) and [Noise-Based Particles, Part II at The Little Grasshopper](http://prideout.net/blog/?p=67)
- [Quasimondo - Mario Klingemann's Flash Blog: Hydra: Noise](http://www.quasimondo.com/archives/000658.php) - sine noise
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/morenoise/morenoise.htm) - advanced value noise
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/voronoise/voronoise.htm) - voronoise. Use [Voronoi](Voronoi)
- [4D Noise Visualizer](http://dyadstudios.com/code/4dnoise/) - 4D noise with GLSL shader. Use a cube with 50x50x50 vertices
- [Playing With Chaos: The Book](http://www.playingwithchaos.net/)
- [Simplex noise - Wikipedia](https://en.wikipedia.org/wiki/Simplex_noise)
- [jwagner/simplex-noise.js: A fast simplex noise implementation in Javascript.](https://github.com/jwagner/simplex-noise.js)

```as3
function Noise(int x, int y)
{
	int n = x + y * 57;
	n = (n<<13) ^ n;

	return ( 1.0 - ( (n * (n * n * r1 + r2) + r3) & 0x7fffffff) / 1073741824.0);
}
```

```glsl
// 1D, 2D & 3D Value Noise
// From http://editor.thebookofshaders.com/?log=170202213311
// Based on Morgan McGuire @morgan3d
// https://www.shadertoy.com/view/4dS3Wd
float noise (in vec2 _st) {
    vec2 i = floor(_st);
    vec2 f = fract(_st);

    // Four corners in 2D of a tile
    float a = random(i);
    float b = random(i + vec2(1.0, 0.0));
    float c = random(i + vec2(0.0, 1.0));
    float d = random(i + vec2(1.0, 1.0));

    vec2 u = f * f * (3.0 - 2.0 * f);

    return mix(a, b, u.x) + 
            (c - a)* u.y * (1.0 - u.x) + 
            (d - b) * u.x * u.y;
}
```

- http://www.connectedpixel.com/blog/texture/wood

```c
/* coherent noise function over 1, 2 or 3 dimensions */
/* (copyright Ken Perlin) */

#include <stdlib.h>
#include <stdio.h>
#include <math.h>

#define B 0x100
#define BM 0xff

#define N 0x1000
#define NP 12   /* 2^N */
#define NM 0xfff

static p[B + B + 2];
static float g3[B + B + 2][3];
static float g2[B + B + 2][2];
static float g1[B + B + 2];
static start = 1;

static void init(void);

#define s_curve(t) ( t * t * (3. - 2. * t) )

#define lerp(t, a, b) ( a + t * (b - a) )

#define setup(i,b0,b1,r0,r1)\
	t = vec[i] + N;\
	b0 = ((int)t) & BM;\
	b1 = (b0+1) & BM;\
	r0 = t - (int)t;\
	r1 = r0 - 1.;
	
double noise1(double arg)
{
	int bx0, bx1;
	float rx0, rx1, sx, t, u, v, vec[1];
	
	vec[0] = arg;
	if (start) {
		start = 0;
		init();
	}
	
	setup(0, bx0,bx1, rx0,rx1);
	
	sx = s_curve(rx0);
	
	u = rx0 * g1[ p[ bx0 ] ];
	v = rx1 * g1[ p[ bx1 ] ];
	
	return lerp(sx, u, v);
}

float noise2(float vec[2])
{
	int bx0, bx1, by0, by1, b00, b10, b01, b11;
	float rx0, rx1, ry0, ry1, *q, sx, sy, a, b, t, u, v;
	register i, j;
	
	if (start) {
		start = 0;
		init();
	}
	
	setup(0, bx0,bx1, rx0,rx1);
	setup(1, by0,by1, ry0,ry1);
	
	i = p[ bx0 ];
	j = p[ bx1 ];
	
	b00 = p[ i + by0 ];
	b10 = p[ j + by0 ];
	b01 = p[ i + by1 ];
	b11 = p[ j + by1 ];
	
	sx = s_curve(rx0);
	sy = s_curve(ry0);
	
#define at2(rx,ry) ( rx * q[0] + ry * q[1] )

	q = g2[ b00 ] ; u = at2(rx0,ry0);
	q = g2[ b10 ] ; v = at2(rx1,ry0);
	a = lerp(sx, u, v);
	
	q = g2[ b01 ] ; u = at2(rx0,ry1);
	q = g2[ b11 ] ; v = at2(rx1,ry1);
	b = lerp(sx, u, v);
	
	return lerp(sy, a, b);
}

float noise3(float vec[3])
{
	int bx0, bx1, by0, by1, bz0, bz1, b00, b10, b01, b11;
	float rx0, rx1, ry0, ry1, rz0, rz1, *q, sy, sz, a, b, c, d, t, u, v;
	register i, j;
	
	if (start) {
		start = 0;
		init();
	}
	
	setup(0, bx0,bx1, rx0,rx1);
	setup(1, by0,by1, ry0,ry1);
	setup(2, bz0,bz1, rz0,rz1);
	
	i = p[ bx0 ];
	j = p[ bx1 ];
	
	b00 = p[ i + by0 ];
	b10 = p[ j + by0 ];
	b01 = p[ i + by1 ];
	b11 = p[ j + by1 ];
	
	t  = s_curve(rx0);
	sy = s_curve(ry0);
	sz = s_curve(rz0);
	
	#define at3(rx,ry,rz) ( rx * q[0] + ry * q[1] + rz * q[2] )

	q = g3[ b00 + bz0 ] ; u = at3(rx0,ry0,rz0);
	q = g3[ b10 + bz0 ] ; v = at3(rx1,ry0,rz0);
	a = lerp(t, u, v);
	
	q = g3[ b01 + bz0 ] ; u = at3(rx0,ry1,rz0);
	q = g3[ b11 + bz0 ] ; v = at3(rx1,ry1,rz0);
	b = lerp(t, u, v);
	
	c = lerp(sy, a, b);
	
	q = g3[ b00 + bz1 ] ; u = at3(rx0,ry0,rz1);
	q = g3[ b10 + bz1 ] ; v = at3(rx1,ry0,rz1);
	a = lerp(t, u, v);
	
	q = g3[ b01 + bz1 ] ; u = at3(rx0,ry1,rz1);
	q = g3[ b11 + bz1 ] ; v = at3(rx1,ry1,rz1);
	b = lerp(t, u, v);
	
	d = lerp(sy, a, b);
	
	return lerp(sz, c, d);
}

static void normalize2(float v[2])
{
	float s;
	
	s = sqrt(v[0] * v[0] + v[1] * v[1]);
	v[0] = v[0] / s;
	v[1] = v[1] / s;
}

static void normalize3(float v[3])
{
	float s;
	
	s = sqrt(v[0] * v[0] + v[1] * v[1] + v[2] * v[2]);
	v[0] = v[0] / s;
	v[1] = v[1] / s;
	v[2] = v[2] / s;
}

static void init(void)
{
	int i, j, k;
	
	for (i = 0 ; i < B ; i++) {
		p[i] = i;
		
		g1[i] = (float)((random() % (B + B)) - B) / B;
		
		for (j = 0 ; j < 2 ; j++)
			g2[i][j] = (float)((random() % (B + B)) - B) / B;
		normalize2(g2[i]);
		
		for (j = 0 ; j < 3 ; j++)
			g3[i][j] = (float)((random() % (B + B)) - B) / B;
		normalize3(g3[i]);
	}
	
	while (--i) {
		k = p[i];
		p[i] = p[j = random() % B];
		p[j] = k;
	}
	
	for (i = 0 ; i < B + 2 ; i++) {
		p[B + i] = p[i];
		g1[B + i] = g1[i];
		for (j = 0 ; j < 2 ; j++)
			g2[B + i][j] = g2[i][j];
		for (j = 0 ; j < 3 ; j++)
			g3[B + i][j] = g3[i][j];
	}
}
```

### Curl Noise

Aka 3D noise

- https://github.com/cabbibo/glsl-curl-noise
- [Shifting sands: Intro to Curl Noise](http://petewerner.blogspot.fr/2015/02/intro-to-curl-noise.html) - see [Curl Noise Slides](https://raw.githubusercontent.com/petewerner/misc/master/Curl%20Noise%20Slides.pdf)

### Sinusoids combination

Could use [Diamond-square algorithm](Algorithms#diamond-square) to do the same effect, but often use a combination of multiple sinusoids

- [Plasma effect — Wikipedia](https://en.wikipedia.org/wiki/Plasma_effect)
- [0ldskool Plasma Effect - Bidouille.org](http://www.bidouille.org/prog/plasma)

## Dithering

![Dithering](Dithering/dithering.png)

- [Dither — Wikipedia](https://en.wikipedia.org/wiki/Dither)
- [Ordered dithering — Wikipedia](https://en.wikipedia.org/wiki/Ordered_dithering)
- [Color quantization — Wikipedia](https://en.wikipedia.org/wiki/Color_quantization)
- [Image Dithering: Eleven Algorithms and Source Code - Tanner Helland (dot) Com](http://www.tannerhelland.com/4660/dithering-eleven-algorithms-source-code/)
- [//game dev log of martins upitis: GLSL dithering](http://devlog-martinsh.blogspot.fr/2011/03/glsl-dithering.html)
- [Posterization — Wikipedia](https://en.wikipedia.org/wiki/Posterization)
- [Quantization -- IM v6 Examples](http://www.imagemagick.org/Usage/quantize/#ordered-dither)
- [JS Bin - Collaborative JavaScript Debugging](http://jsbin.com/iXofIji/2/edit?html,css,js,output)
- [OpenSource Image Dithering for AS3. (demo+source). | UnitZeroOne](http://unitzeroone.com/blog/2008/05/06/opensource-image-dithering-for-as3-demosource/) [imageditheringas3](https://code.google.com/archive/p/imageditheringas3/)
- [Sphere surface uniform random sampling](Sphere surface uniform random sampling.html) - see [Román Cortés » Furbee - My Js1k Spring ‘13 entry](http://www.romancortes.com/blog/furbee-my-js1k-spring-13-entry/)
- [Floyd Steinberg dithering](https://codepen.io/nicoptere/pen/waPOOm)

## Random

Aka random number, pseudo random number (PRN)

See also [Noise](#noise)

- [nquinlan/better-random-numbers-for-javascript-mirror: A direct mirror of Johannes Baagøe's wiki on implementations of Randomness in Javascript.](https://github.com/nquinlan/better-random-numbers-for-javascript-mirror)
- [Poisson distribution — Wikipedia](https://en.wikipedia.org/wiki/Poisson_distribution)
- [Better, smaller and faster random number generator](http://www.rgba.org/articles/sfrand/sfrand.htm)
- unsigned 32-bit seed `n`, `n*=0x9e3779b1;` (`0x9e3779b1` is just a large prime number specified in hexadecimal). See [14 Character Random Number Generator](http://theorangeduck.com/page/14-character-random-number-generator)
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/sfrand/sfrand.htm) - float, small and random
- [When Random Numbers Are Too Random: Low Discrepancy Sequences « The blog at the bottom of the sea](https://blog.demofox.org/2017/05/29/when-random-numbers-are-too-random-low-discrepancy-sequences/)
- [nquinlan/better-random-numbers-for-javascript-mirror: A direct mirror of Johanne Baagøe' wiki on implementation of Randomnes in Javascript.](https://github.com/nquinlan/better-random-numbers-for-javascript-mirror)
- [Better random number for javascript - JBWiki](https://web.archive.org/web/20120619002808/baagoe.org/en/wiki/Better_random_numbers_for_javascript)
- [coverslide/node-alea: A simple copy-and-paste implementation of Johanne Baagøe' Alea PRNG](https://github.com/coverslide/node-alea)
- [Park-Miller-Carta Pseudo-Random Number Generators](http://www.firstpr.com.au/dsp/rand31/)

Random points on the sphere surface (see also [Sphere Point Picking](https://mathworld.wolfram.com/SpherePointPicking.html)):

> The way to correctly generate a random point on the surface of a unit sphere is not to pick uniform distributions θ in [0,2π) and φ in [0,π), but instead choose u and v from uniform distributions on [0,1). Then
> 
> φ = cos⁻¹(2v-1)
> θ = 2πu
> — [Fermat's Library on Twitter: "The way to correctly generate a random point on the surface of a unit sphere is not to pick uniform distributions θ in \[0,2π) and φ in \[0,π), but instead choose u and v from uniform distributions on \[0,1). Then φ = cos⁻¹(2v-1) θ = 2πu https://t.co/Y6IX23ZGIv" / Twitter](https://twitter.com/fermatslibrary/status/1238088369420357633?s=12)

```js
// Mulberry32 pseudo random number generator (same result every time)
// example:
// const pseudoRandom = new mulberry32(12345678); // seed it
// const x = pseudoRandom(); // same as Math.random() but the same each time
// see https://stackoverflow.com/questions/521295/
function mulberry32(a){
    return function(){
        let t = a += 0x6D2B79F5;
        t = Math.imul(t ^ t >>> 15, t | 1);
        t ^= t + Math.imul(t ^t >>> 7, t | 61);
        return ((t ^t >>> 14) >>> 0) / 4294967296;
    }
}

```

```js
W=200; I=2; J=2;
Math.random()*W 2)
Math.cos(++I*I)*W 3)
++J**5%W
// [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/cihowe/edit?css,js,output)
```

```js
var seed = 1;
// Implementation of Park-Miller-Carta PRNG ported from http://lab.polygonal.de/2007/04/21/a-good-pseudo-random-number-generator-prng/
function random(seed) {
	seed = (seed * 16807) % 2147483647;
	return seed / 2147483647;
}
```

```as3
package net.dotswitch.math {
	import flash.errors.IllegalOperationError;
	
	public class Random {
		
		public function Random() {
			throw new IllegalOperationError("Illegal instantiation: Random.");
		}
		
		
		// just alias
		public static function random():Number {
			return Math.random();
		}
		
		public static function randomPair():Array {
			return [random(), random()];
		}
		
		
		public static function uniform():Number {
			return 2.0 * Math.random() - 1.0;
		}
		
		public static function uniformPair():Array {
			return [uniform(), uniform()];
		}
		
		
		public static function gaussian():Number {
			return gaussianPair()[0];
		}
		
		public static function gaussianPair():Array {
			var x1:Number, x2:Number, w:Number;
			
			do {
				x1 = uniform();
				x2 = uniform();
				w = x1 * x1 + x2 * x2;
			} while (w >= 1.0)
			
			w = Math.sqrt(-2.0 * Math.log(w) / w);
			
			return [x1 * w, x2 * w];
		}
	
	
		public static function spherical():Array {
			var theta:Number = 2.0 * Math.PI * Math.random();
			var z:Number = uniform();
			
			var c:Number = Math.sqrt(1 - z * z);
			
			var x:Number = c * Math.cos(theta);
			var y:Number = c * Math.sin(theta);
			
			return [x, y, z];
		}
	}
}
```

## Suffle

Aka randomize, random permutation

- [The Danger of Naïveté](https://blog.codinghorror.com/the-danger-of-naivete/)
- [Fisher–Yates shuffle — Wikipedia](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)
- [Fisher–Yates Shuffle](https://bost.ocks.org/mike/shuffle/)
- [How to randomize (shuffle) a JavaScript array? - Stack Overflow](https://stackoverflow.com/questions/2450954/how-to-randomize-shuffle-a-javascript-array/2450976#2450976)

## 3D volume distribution

- [3D volume distribution – Youpi !](http://barradeau.com/blog/?p=1058)

## Procedural

- Texturing and Modeling: A Procedural Approach — David S. Ebert 978-1558608481
- https://watabou.itch.io/medieval-fantasy-city-generator

## Visual representation of MD5 hash

- [PHP Identicons download | SourceForge.net](https://sourceforge.net/projects/identicons/)
- [FrancisShanahan/Identicon5](https://github.com/FrancisShanahan/Identicon5)
