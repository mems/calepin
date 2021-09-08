Aka animation

`Position= (gravity*time^2)/2` (same as `P= (g*t^2)/2`)

Normal gravity: -9.8m/s2

- [Bullet Physics SDK](https://github.com/bulletphysics/bullet3) - real-time collision detection and multi-physics simulation for VR, games, visual effects, robotics, machine learning etc. See [Real-Time Physics Simulation](http://bulletphysics.org/wordpress/)
- [Coder Corner » Archivio Blog » The evolution of PhysX - Index](http://www.codercorner.com/blog/?p=914%20)

![Vehicule Rotation](vehicule%20rotation.png)

## Fracture

Aka Destructible 3D Objects, break, shattering object, spliting, Dynamic Fracture with Convex Decompositions

Ex: From bullet

Voronoi cells can be used

Particles can be use for additional effect, smoke, etc.

- [Real Time Dynamic Fracture with Volumetric Approximate Convex Decompositions - YouTube](https://www.youtube.com/watch?v=eB2iBY-HjYU) - see [Real Time Dynamic Fracture ith Volumetric Approximate Convex Decompositions - fractureSG2013.pdf](http://matthias-mueller-fischer.ch/publications/fractureSG2013.pdf)
- [GPU-Accelerated Dynamic Fracture in the Browser - CIS 565 Final Project](https://github.com/kainino0x/cis565final) - use WebCL
- [Bricks breaking example](http://yomboprime.github.io/GPGPU-threejs-demos/webgl_physics_convex_break.html)
- [A Cracking Algorithm for Destructible 3D Objects - download](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.138.8659&rep=rep1&type=pdf)

## Cloth simulation

- [OpenCloth Textured WebGL Demo by Movania Muhammad Mobeen](https://cdn.rawgit.com/mmmovania/opencloth/5db9b1c5/OpenCloth_WebGL/WebGLOpenClothTextured.html) and [A collection of source codes implementing cloth simulation algorithms in OpenGL](https://github.com/mmmovania/opencloth) - see Wiki on [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/opencloth/wikis)
- [Drape - a cloth simulator](https://cdn.rawgit.com/aatishb/drape/df7db9ef/index.html) - Drape WebGL simulation. See https://github.com/aatishb/drape

## GPU physics

- [quadtree 3](https://www.shadertoy.com/view/lljSDy)
- [tritree](https://www.shadertoy.com/view/Mt2XDc)
- [GPU Gems | NVIDIA Developer](https://developer.nvidia.com/gpugems/GPUGems3/gpugems3_ch29.html)
- [OpenCL Game Physics](http://www.nvidia.com/content/gtc/documents/1077_gtc09.pdf)
- [WebGL Particles](http://nullprogram.com/webgl-particles/) - [skeeto/webgl-particles: WebGL particle system demo](https://github.com/skeeto/webgl-particles)
- [A GPU Approach to Particle Physics « null program](http://nullprogram.com/blog/2014/06/29/)
- [Are GPU physics implementations branchless? - Game Development Stack Exchange](https://gamedev.stackexchange.com/questions/98620/are-gpu-physics-implementations-branchless)
- [A GPU Approach to Voronoi Diagrams « null program](http://nullprogram.com/blog/2014/06/01/)
- [Unity Compute Shader Experiments: GPU Physics - YouTube](https://www.youtube.com/watch?v=wf9nadEEmtw)
- [SIMD / GPU Friendly Branchless Binary Search « The blog at the bottom of the sea](https://blog.demofox.org/2017/06/20/simd-gpu-friendly-branchless-binary-search/)

- [Thinking Parallel, Part I: Collision Detection on the GPU | Parallel Forall](https://devblogs.nvidia.com/parallelforall/thinking-parallel-part-i-collision-detection-gpu/)
- [Thinking Parallel, Part II: Tree Traversal on the GPU | Parallel Forall](https://devblogs.nvidia.com/parallelforall/thinking-parallel-part-ii-tree-traversal-gpu/)
- [Thinking Parallel, Part III: Tree Construction on the GPU | Parallel Forall](https://devblogs.nvidia.com/parallelforall/thinking-parallel-part-iii-tree-construction-gpu/)
- [Using GPUs for Collision detection, Recent Advances in Real-Time Coll…](https://www.slideshare.net/takahiroharada/using-gpus-for-collision-detection-recent-advances-in-realtime-collision-and-proximity-computations-for-games-and-simulations-eurographics-2012)
- [FULLTEXT01.pdf](http://umu.diva-portal.org/smash/get/diva2:403566/FULLTEXT01.pdf)
- [Collision-Streams: Fast GPU-based Collision Detection for Deformable Models](http://gamma.cs.unc.edu/CSTREAMS/)

> n-body problem is the problem of predicting the individual motions of a group of celestial objects interacting with each other gravitationally.
— [n-body problem — Wikipedia](https://en.wikipedia.org/wiki/N-body_problem)

- [GPU gems to Unity: NBody simulation | ScrawkBlog](http://web.archive.org/web/20151006013850/http://scrawkblog.com/2014/02/07/gpu-gems-to-unity-nbody-simulation/)
- [Unity Web Player | gravitySIm](http://www.pjhodson.com/nbody/web.html) - [pjhodson/unity3D-nbody-grav: Basic N-Body Gravitational Simulation in Unity](https://github.com/pjhodson/unity3D-nbody-grav)
- [Scrawk/GPU-GEMS-NBody-Simulation: A NBody simulation in Unity](https://github.com/Scrawk/GPU-GEMS-NBody-Simulation)
- [n-Body Galaxy Simulation using Compute Shaders on GPGPU via Unity 3D | MickyD's Random Thoughts](https://mickyd.wordpress.com/2014/02/01/n-body-galaxy-simulation-using-compute-shaders-on-gpgpu-via-unity-3d/)

Possible implementation: physical model is based on repulsion. Overlapping bodies in a grid cell add a repulsion force to each other

## Motion

Aka velocity, acceleration, force, torque

- [Description of Motion](https://web.archive.org/web/20210629104702/http://hyperphysics.phy-astr.gsu.edu/hbase/mot.html#mot2)

### Friction

- [math - Simple physics-based movement - Stack Overflow](https://stackoverflow.com/questions/667034/simple-physics-based-movement/667090#667090)
- [physics - Find coefficient of static friction if given initial velocity and distance? - Mathematics Stack Exchange](https://math.stackexchange.com/questions/534717/find-coefficient-of-static-friction-if-given-initial-velocity-and-distance)
- [Modeling gravity and friction (article) | Khan Academy](https://www.khanacademy.org/computing/computer-programming/programming-natural-simulations/programming-forces/a/modeling-gravity-and-friction)
- [Braking distance — Wikipedia](https://en.wikipedia.org/wiki/Braking_distance)
- [Stopping Distance Formula | Formula for Stopping Distance | Formulas@TutorVista.com](http://formulas.tutorvista.com/physics/stopping-distance-formula.html)
- [homework and exercises - How to find stopping distance of a car? - Physics Stack Exchange](https://physics.stackexchange.com/questions/167003/how-to-find-stopping-distance-of-a-car)
- [Speed and Velocity](http://www.physicsclassroom.com/class/1DKin/Lesson-1/Speed-and-Velocity)
- [Calculating average velocity or speed (video) | Khan Academy](https://www.khanacademy.org/science/physics/one-dimensional-motion/displacement-velocity-time/v/calculating-average-velocity-or-speed)

From [Math time: Resting position · Metafizzy blog](https://metafizzy.co/blog/math-time-resting-position/):

```js
function baseLog( a, b ) {
	return Math.log( b ) / Math.log( a );
}

class Particle{
	constructor( x, y ) {
		this.x = x;
		this.y = y;
		this.velocity = 0;
		this.accel = 0;
		this.friction = 0.2;
	}

	update() {
		this.velocity += this.accel;
		this.velocity *= ( 1 - this.friction );
		this.x += this.velocity;
		this.accel = 0;
	}

	applyForce( force ) {
		this.accel += force;
	}

	// Euler method
	getRestingPosition() {
		// little simulation where thing will rest
		let restingVelo = 0.07;
		let velo = this.velocity;
		let restX = this.x;
		while ( Math.abs( velo ) > restingVelo ) {
			velo *= 1 - this.friction;
			restX += velo;
		}
		return restX;
	}

	// Math version
	getRestingPosition() {
		// get how many ticks until velocity is slow
		var restingVelo = 0.07; // ideally, this is 0, but that would take infinite amount of ticks
		var fFriction = 1 - this.friction;
		var ticks = baseLog( fFriction, restingVelo / Math.abs( this.velocity ) );
		// integrate to determine resting position
		var sum = ( Math.pow( fFriction, ticks + 1 ) - 1 ) / ( fFriction - 1 );
		// additional fFriction to account for initial tick
		return this.x + this.velocity * fFriction * sum;
	}
}

let estimateX = 0;
let canvas = document.createElement("canvas");
let ctx = canvas.getContext('2d');
let canvasW = canvas.width = window.innerWidth - 20;
let canvasH = canvas.height = window.innerHeight - 80;
document.body.appendChild(canvas);
canvas.addEventListener( 'mousedown', onMousedown, false );
let particle = new Particle( canvasW / 2, canvasH / 2 );

// -------------------------- animate, render, update -------------------------- //
function animate() {
	particle.update();
	// wrap around
	if ( !isDragging ) {
	  particle.x = ( particle.x + canvasW ) % canvasW;
	}
	render();
	requestAnimationFrame( animate );
}

function render() {
	ctx.clearRect( 0, 0, canvasW, canvasH );

	// render particle
	ctx.fillStyle = 'hsla(0, 100%, 50%, 0.5)';
	circle( particle.x, particle.y, 15 );

	// render estimate
	ctx.fillStyle = 'hsla(150, 100%, 25%, 0.5)';
	// wrap around
	estimateX = ( estimateX + canvasW ) % canvasW;
	circle( estimateX, canvasH / 2, 10 );
}

function circle( x, y, radius ) {
	ctx.beginPath();
	ctx.arc( x, y, radius, 0, Math.PI * 2, true );
	ctx.fill();
	ctx.closePath();
}

// -------------------------- mouse -------------------------- //
let isDragging = false;

function onMousedown( event ) {
	event.preventDefault();
	isDragging = true;
	window.addEventListener( 'mousemove', onMousemove, false );
	window.addEventListener( 'mouseup', onMouseup, false );
	particle.x = event.pageX;
	particle.velocity = 0;
}

let previousX;
let previousTime;
let currentTime;

function onMousemove( event ) {
	// previous
	previousX = particle.x;
	previousTime = currentTime;
	// current
	particle.x = event.pageX;
	currentTime = new Date();
}

function onMouseup( event ) {
	if ( previousX ) {
		particle.velocity = ( particle.x - previousX ) / ( currentTime - previousTime );
		particle.velocity *= 17;
		estimateX = particle.getRestingPosition();
		previousX = null;
	}

	isDragging = false;
	window.removeEventListener( 'mousemove', onMousemove, false );
	window.removeEventListener( 'mousemove', onMouseup, false );
}

animate();
```

Pulse:

```js
/***********************************************
 * PULSE (by Michael Herf)
 ***********************************************/

/**
 * Viscous fluid with a pulse for part and decay for the rest.
 * - Applies a fixed force over an interval (a damped acceleration), and
 * - Lets the exponential bleed away the velocity over a longer interval
 * - Michael Herf, http://stereopsis.com/stopping/
 */
function pulse_(x) {
	var val, start, expx;
	// test
	x = x * options.pulseScale;
	if (x < 1) { // acceleartion
		val = x - (1 - Math.exp(-x));
	} else {	 // tail
		// the previous animation ended here:
		start = Math.exp(-1);
		// simple viscous drag
		x -= 1;
		expx = 1 - Math.exp(-x);
		val = start + (expx * (1 - start));
	}
	return val * options.pulseNormalize;
}

function pulse(x) {
	if (x >= 1) return 1;
	if (x <= 0) return 0;

	if (options.pulseNormalize == 1) {
		options.pulseNormalize /= pulse_(1);
	}
	return pulse_(x);
}
```

- [stereopsis : How to make things stop](http://stereopsis.com/stopping/)

### Gravity

- https://www.reddit.com/r/programming/comments/4sc5wz/i_finished_my_gravity_simulator_it_is_now_open/ and https://github.com/larsXYZ/Gravity-Simulator

> 	double aks = 0;
> 	double angle = atan2(dy, dx);
> 	if (dist != 0) aks = G * pListe[p].getmass() / (dist*dist);
> 	pListe[i].getxv() += cos(angle) * aks * tidsskritt;
> 	pListe[i].getyv() += sin(angle) * aks * tidsskritt;
>
> Why all these atan, cos and sin? Isn't just `cos(angle) = dx / dist`?
>
> Also, you don't conserve momentum when there are any explosions. If some planet explodes you break the loop and forget to think about the following planets and their influence.

Use euler integration

- [Fluxions for Fun and Profit: Euler, Trapezoidal, Verlet, or Runge-Kutta? - Jason Sachs](https://www.embeddedrelated.com/showarticle/474.php)
- http://www.nowykurier.com/toys/gravity/gravity.swf
- https://bitbucket.org/jason_s/jason_s.bitbucket.org/src/d6a11a019045/gravity1/?at=default http://wayback.archive.org/web/20131005021057/http://jason_s.bitbucket.org/gravity1/
- [Gravity Calculations - Falling Body Equations at gravitycalc.com](http://www.gravitycalc.com/)
- [newtonian mechanics - How does force relate to velocity? - Physics Stack Exchange](https://physics.stackexchange.com/questions/17049/how-does-force-relate-to-velocity)

- [JS1k, 1k demo submission by @Flexi23 - Spring is here again!](http://cake23.de/js1k-spring.html)
- [Matter.js Simple Ball Pool](http://www.cake23.de/matterjs-simple-ball-pool.html)
- [Particle system example](http://paulbourke.net/miscellaneous/particle/)
- [Physics - Kinematics - Angular Velocity - Martin Baker](http://www.euclideanspace.com/physics/kinematics/angularvelocity/quatDiff1stAttempt.htm)
- [sigsegv - YouTube](https://www.youtube.com/channel/UCAryhnkzHOMkir-F2PsMBVQ/videos) - Physics in TF2
- [shiffman/The-Nature-of-Code-Examples: Repository for example code from The Nature of Code book](https://github.com/shiffman/The-Nature-of-Code-Examples) - see also [Port the nature of code examples to raphael](http://deadhorse.me/the-nature-of-code-raphael/)
- [matter-attractors demo](https://liabru.github.io/matter-attractors/#basic) - [liabru/matter-attractors: an attractors plugin for matter.js](https://github.com/liabru/matter-attractors)
- [what power](https://codepen.io/ge1doot/pen/LpLLQa) - rag doll
- [Simple Verlet Physics Engine](https://codepen.io/ge1doot/pen/doXvge) - Simple Verlet Physics Engine

#### Tower of Lire

- [How a Tower of Lire works - GIF on Imgur](http://imgur.com/gallery/iBm7kXA)
- [Book Stacking Problem -- from Wolfram MathWorld](http://mathworld.wolfram.com/BookStackingProblem.html)
- [MathCS.org - Real Analysis: Example 4.1.10: The Leaning Tower of Lire](http://www.mathcs.org/analysis/reals/numser/answers/lire_tower.html)

### Kinetic energy

```
K = (1/2) M v²
```

where `K` is the kinetic energy, `M` is the mass, and `v` is its velocity. The power

```
P = K/t
```

- [Can the teardrops that fall after reading bad science writing generate renewable electricity? Yes, they can. – The Eighteenth Elephant](https://eighteenthelephant.com/2020/02/12/can-the-teardrops-that-fall-after-reading-bad-science-writing-generate-renewable-electricity-yes-they-can/)
