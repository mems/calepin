See also [Physics](Physics)

- [FN1403001 | バネのような動きを加速度から定める ー オイラー法 | HTML5 : テクニカルノート](http://www.fumiononaka.com/Business/html5/FN1403001.html)
- https://github.com/MengTo/Spring/blob/master/Spring/Spring.swift

## Resources

- [The ultimate guide to proper use of animation in UX](https://uxdesign.cc/the-ultimate-guide-to-proper-use-of-animation-in-ux-10bd98614fa9)
- [12 basic principles of animation — Wikipedia](https://en.wikipedia.org/wiki/12_basic_principles_of_animation)
- [Creating Usability with Motion: The UX in Motion Manifesto](https://medium.com/@ux_in_motion/creating-usability-with-motion-the-ux-in-motion-manifesto-a87a4584ddc)
- [CAPPTIVATE.co | iOS UI Animations](http://capptivate.co/)
- [Hover States / The home of alternative digital design](http://hoverstat.es/)
- [Motion blur — Wikipedia](https://en.wikipedia.org/wiki/Motion_blur)

## The illusion of life

![The illusion of life_hd.mp4](The illusion of life_hd.mp4)
![10 principles of motion design.mp4](10 principles of motion design.mp4)

## Precision

Eular method is frame based
More precise is time based

The Eular method simplifies equation:

	position += velocity * dt;
	velocity += acceleration * dt;

The semi-implicit euler (better):

	velocity += acceleration * dt;
	position += velocity * dt;

frame skip = based on time
non frame skip = based on number frames. It's not precise especially if the frame rate is irregular or not at the original speed

[Recusive functions](https://en.wikipedia.org/wiki/Recursive_function) are frame based

Eular method:

	let threshold = 0.07;// resting velocity
	let friction = 0.15;
	let x = 0;
	let velocity = 30;
	
	// loop is an equivalent to call a render frame function
	while ( velocity > threshold ) {
		velocity *= 1 - friction;
		x += velocity;
	}
	return x;

See also:

	static double lastUpdate=0;
	if (lastUpdate!=0) {
		deltaT = time() - lastUpdate;
		velocity += acceleration * deltaT;
		position += velocity * deltaT;
	}
	lastUpdate = time();

Time based (use integration and calculus):

	var restingVelo = 0.07;
	var startVelo = 30;
	var friction = 0.15;
	var startX = 0;
	
	function getBaseLog( a, b ) {
	  return Math.log( b ) / Math.log( a );
	}
	
	let damping = 1 - friction;
	let ticks = getBaseLog( damping, restingVelo / Math.abs( startVelo ) );
	// http://mikestoolbox.com/powersum.html
	let sum = ( Math.pow( damping, ticks + 1 ) - 1 ) / ( damping - 1 );
	x += startVelo * damping * sum;

- [Integration Basics | Gaffer On Games](https://gafferongames.com/post/integration_basics/)
- [Fix Your Timestep! | Gaffer On Games](https://gafferongames.com/post/fix_your_timestep/)
- [Physics for Flash Games](http://www.richardlord.net/presentations/physics-for-flash-games.html) - difference between integrator
- [physics - Pros and cons of different integrators - Game Development Stack Exchange](https://gamedev.stackexchange.com/questions/33694/pros-and-cons-of-different-integrators)
- [PhysicsJS/src/integrators at master · wellcaffeinated/PhysicsJS](https://github.com/wellcaffeinated/PhysicsJS/tree/master/src/integrators) - Implementation of different integrators in PhysicsJS
- [Matter.js Simple Ball Pool](http://www.cake23.de/matterjs-simple-ball-pool.html)
- [Loop vs log · jsPerf](https://jsperf.com/loop-vs-log/)

## Eular method

- [Euler method — Wikipedia](https://en.wikipedia.org/wiki/Euler_method)

### Inching

Aka Ease out animation

> position += (destination - position) * friction

	ease = 0.25;
	position = 0;
	destination = 100;
	
	frame{
		velocity = (destination - position) * ease;
		position += velocity;
	}

### Elastic

[Simple harmonic motion — Wikipedia](https://en.wikipedia.org/wiki/Simple_harmonic_motion)

	ease = 0.25;
	velocity = 0;
	friction = 0.75;
	position = 0;
	destination = 100;
	
	frame{
		velocity += (destination - position) * ease;
		velocity *= friction;
		position += velocity;
	}

### Flexible Partial Shifts

	var dx:Number = displayObject.x - fixedX;
	var dy:Number = displayObject.y - fixedY;
	var angle:Number = Math.atan2(dy, dx);
	var targetX:Number = fixedX + Math.cos(angle) * springLength;
	var targetY:Number = fixedX + Math.sin(angle) * springLength;

### Waveform

	displayObject.y = centerScale + Math.sin(angle) * range;
	angle += speed;

### Heartthrob

	displayObject.scaleX = displayObject.scaleY = centerScale + Math.sin(angle) * range;
	angle += speed;

## Easing

See also [Catmull–Rom spline](Spline) and [Gradient](Gradient)

- [Easing Functions Cheat Sheet](http://easings.net/en)
- [Equations for Organic Motion](http://codepen.io/soulwire/pen/kqHxB)
- https://github.com/greensock/GreenSock-JS/blob/master/src/uncompressed/easing/EasePack.js
- [A Performant Transitions and Animations Library](https://github.com/h5bp/Effeckt.css)
- [Inbetweening — Wikipedia](https://en.wikipedia.org/wiki/Inbetweening)
- [Tweener, 4 years later – A post mortem – Zeh Fernando](http://zehfernando.com/2009/tweener-4-years-later-a-post-mortem/)
- [Animation Principles in UI Design: Understanding Easing – Motion In Interaction – Medium](https://medium.com/motion-in-interaction/animation-principles-in-ui-design-understanding-easing-bea05243fe3)
- [Understanding Easing (Explaining Penner’s equations) – JavaScript and ActionScript | upshots](http://upshots.org/actionscript/jsas-understanding-easing)
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/functions/functions.htm) - useful little functions
- [Better Cubic Bezier Approximations for Robert Penner Easing Equations | kepo-ing Zz85](http://www.lab4games.net/zz85/blog/2014/12/26/better-cubic-bezier-approximations-for-robert-penner-easing-equations/) - see https://github.com/zz85/cubic-bezier-approximations
- [Ease Visualizer for GSAP | HTML5 Animation | GreenSock](https://greensock.com/ease-visualizer)
- [phaser/v3/src/math/easing at master · photonstorm/phaser](https://github.com/photonstorm/phaser/tree/master/v3/src/math/easing)
- [curves | kynd.info | Flickr](https://www.flickr.com/photos/kynd/9546075099/) - Easing functions/equations https://farm8.staticflickr.com/7346/9546075099_18ccc66a2d_o_d.png
- [scripty2 API documentation | S2.FX.Transitions namespace](http://scripty2.com/doc/scripty2%20fx/s2/fx/transitions.html)

- `sin(t)`
- `cos(t)`
- `cos(t)*sin(t)`
- `sin(t)*sin(t*1.5)`
- `sin(tan(cos(t)*1.2))`
- `sin(tan(t)*0.05)`
- `cos(sin(t*3))*sin(t*0.2)`
- `sin(pow(8,sin(t)))`
- `sin(exp(cos(t*0.8))*2)`
- `sin(t-PI*tan(t)*0.01)`
- `pow(sin(t*PI),12)`
- `cos(sin(t)*tan(t*PI)*PI/8)`
- `sin(tan(t)*pow(sin(t),10))`
- `cos(sin(t*3)+t*3)`
- `pow(abs(sin(t*2))*0.6,sin(t*2))*0.6`
- ... (see links above)
- `cos(pi*x) / (-LN2*x)`
- `sqrt(1-x^2)` Semi arc (* -1 to get negative)
- `1-pow(x*2-1, 6)` smooth in-out, use power of 2, 4, 6, etc. to make the transition sharper


- Linear (Power0)
- Quad (Power1)
- Cubic (Power2)
- Quart (Power3)
- Quint (Power4)
- Strong (Power4)

### Time progression

	progress = max(min((nowTimestamp - timestamp) / duration, 1), 0);// 0 to 1

## Animation duration

- [How fast should your UI animations be? | Val Head - Designer & UI Animation Consultant](http://valhead.com/2016/05/05/how-fast-should-your-ui-animations-be/)

## Physics based

Animation based on physics

Use friction, attraction force (gravity, magnetism), push force
Mass, velocity (speed + direction), momentum

See [Physics](Physics)

- [The Nature of Code](http://natureofcode.com/book/)
- Lib for lot of domains (math, graphics) https://github.com/hapticdata/toxiclibsjs from http://toxiclibs.org/about/
- https://en.wikipedia.org/wiki/Physics_engine
- A posteriori (discrete) versus a priori (continuous) computation: https://en.wikipedia.org/wiki/Collision_detection#A_posteriori_.28discrete.29_versus_a_priori_.28continuous.29
- https://openclassrooms.com/courses/theorie-des-collisions

- Parametric easing (easing function with parameters like frequency, friction) http://dynamicsjs.com
- game libs http://phaser.io https://libgdx.badlogicgames.com/index.html
- native JS canvas only lib https://github.com/phoboslab/Ejecta

https://en.wikipedia.org/wiki/Force
https://en.wikipedia.org/wiki/Classical_mechanics

## Cat walking

> Cats have a very precise method of walking, called “direct registering”, wherein their hind paws fall almost exactly into the place their fore paws did a moment before—this method of walking minimizes noise and visible tracks while ensuring more stable footing as the place has already been felt out by the fore paws

- [How a cat makes footprints : interestingasfuck](https://www.reddit.com/r/interestingasfuck/comments/6b3u4n/how_a_cat_makes_footprints/)
- [Animal Gaits for Animators on Vimeo](https://vimeo.com/215637283)

## Draggable with inertia

Scrollable, deceleration, rubber band, paging (aka Soft close drawer)

> Linear Motion Equations:
> 
> vf = vi + at
> d = ½(vf + vi)t
> d = vi∙t + ½at
> vf² = vi² + 2ad
> 
> where:
> 
> - d is displacement (∆x)
> - t is time of travel (∆t)
> - a is rate of constant acceleration
> - vi is initial velocity
> - vf is final velocity
> 
> https://s2.studylib.net/store/data/005704450.pdf?key=7f28457ce04d3cb302b11a2f52dba5b3&r=1&fn=5704450.pdf&t=1536095317883&p=600

Rubber-banding: x = (1.0 - (1.0 / ((x * c / d) + 1.0))) * d or x = x * 0.5

> f(x, d, c) = (x * d * c) / (d + c * x)
> 
> where:
> 
> - x is distance from the edge
> - c is constant (UIScrollView uses 0.55)
> - d is dimension, either width or height

UIScrollView to find out the formulae its using for paging, inertia, and bouncing: rubber banding: offset = (0.55 * offset * height) / (height + 0.55 * offset); inertia: exponential decay with .decelerationRate

- [Implementing Inertial Scrolling in iOS - The Joy Of Hack](http://aijazansari.com/2011/04/25/implementing-inertial-scrolling-in-ios/index.html)
- [ios - UIScrollView with "inertia" but paged. - Stack Overflow](https://stackoverflow.com/questions/20667613/uiscrollview-with-inertia-but-paged/20669439#20669439)
- [CircularScrollInertia/RDDRotationControlSurface.m at master · rdsquared09/CircularScrollInertia](https://github.com/rdsquared09/CircularScrollInertia/blob/master/CircularScrollInertiaDemo/RDDRotationControlSurface.m) - Circular slider [SpinnyDisk on Vimeo](https://vimeo.com/51800558)
- [grp/CustomScrollView: A fork of Ole Begemann's custom scroll view project, that adds decelerated scrolling, just like `UIScrollView`](https://github.com/grp/CustomScrollView/tree/custom-scroll-with-pop) with [facebook/pop: An extensible iOS and OS X animation library, useful for physics-based interactions.](https://github.com/facebook/pop)
- [Grant Paul on Twitter: "I mentioned a while back iOS 6 uses a new formula for rubber-banding. Here's the formula: x = (1.0 - (1.0 / ((x * c / d) + 1.0))) * d"](https://twitter.com/chpwn/status/285540192096497664)
- [UIScrollView's Inertia, Bouncing and Rubber-Banding with UIKit Dynamics](http://holko.pl/2014/07/06/inertia-bouncing-rubber-banding-uikit-dynamics/)
- [Implementing scrolling behaviour without UIScrollView – Successful coder](http://successfulcoder.com/2016/09/04/implementing-scrolling-behaviour-without-uiscrollview/) - (end of article) about need to evaluate multiple touchmove events at the end of gesture to get the velocity desizered
- [Scrolling — Wikipedia](https://en.wikipedia.org/wiki/Scrolling) - "Touch-screens often use inertial scrolling"
- [Inertial Scrolling for Unity 3D](https://gist.github.com/russianryebread/46dc971afe20861e9158)
- [kinetic scrolling: the state machine · ariya.io](https://ariya.io/2009/10/kinetic-scrolling-the-state-machine) - State machine for a slider
- [Creating Animations and Interactions with Physical Models](http://iamralpht.github.io/physics/) https://github.com/iamralpht/iamralpht.github.io/tree/master/physics
- [openseadragon/openseadragon: An open-source, web-based viewer for zoomable images, implemented in pure JavaScript.](https://github.com/openseadragon/openseadragon) - image explorer, zoom use springs [openseadragon/spring.js at master · openseadragon/openseadragon](https://github.com/openseadragon/openseadragon/blob/master/src/spring.js)
- [Framer/LayerDraggable.coffee at master · koenbok/Framer](https://github.com/koenbok/Framer/blob/master/framer/LayerDraggable.coffee)
- [iamralpht/gravitas: A super fast, super small Physics Engine for super awesome User Interface](https://github.com/iamralpht/gravitas)
- [Impetus.js - Add Momentum to Anything](http://chrisbateman.github.io/impetus/)
- [Draggable | GSAP from GreenSock | JavaScript HTML5 Animation](https://greensock.com/draggable) https://github.com/kevinglb/Cartier-Wechat/blob/master/greensock-js/src/uncompressed/utils/Draggable.js https://s3-us-west-2.amazonaws.com/s.cdpn.io/16327/ThrowPropsPlugin.min.js https://github.com/iWoz/AirScroll/blob/master/src/com/greensock/plugins/ThrowPropsPlugin.as
- [Add experimental support for spring based CSS animations](https://trac.webkit.org/changeset/201759/trunk/Source) - see `WebCore/platform/graphics/SpringSolver.h`
- [ScrollMagic/iscroll-probe.js at master · janpaepke/ScrollMagic](https://github.com/janpaepke/ScrollMagic/blob/master/js/lib/iscroll-probe.js#L56-L81)

Like scroll with touch or mouse wheel. See also http://dev.w3.org/csswg/css-snappoints/, [`-ms-scroll-limit`](http://msdn.microsoft.com/en-us/library/windows/apps/hh996918.aspx) (offlimit bounce) and https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/IpBdJEppjzE/V1Biy1D4v-kJ

- [Prototyping with Facebook Origami on Vimeo](https://vimeo.com/85578380)

Scroll time based on distance:

	var baseMinScrollTime = 200;
	var baseMaxScrollTime = 500;
	
	var docHeight = $(document).height();
	var triggerTop = $(this).offset().top;
	var targetTop = $target.offset().top;
	
	var scrollProportion = (targetTop - triggerTop) / docHeight,
	var relativeTime = ((baseMaxScrollTime - baseMinScrollTime) * scrollProportion) + baseMinScrollTime,
	// Create inverse relationship (quicker the further we scroll)
	var scrollTime = -1 * (1 - relativeTime);
	
	$('html, body').animate({
	  scrollTop: targetTop - 10
	}, scrollTime);

Friction:

> vector velocity = speed + direction
> 
> google maps
> Speed decrease like POWER2
> 
> f(x) = 99.9%^x
> 
> drop (a=0→1)
> 
> v = d / t
> where
> v = speed or velocity
> d = distance
> t = time or duration
> 
> stopping distance: start velocity to 0
> d = k * v * v,
> where
> d = distance
> k = friction coef
> v = start speed or velocity
> 
> stopping duration?ranl(fr)
> t = d / v
> t = time or duration
> v = average speed or velocity (= start speed / 2)
> d = distance

- [Math time: Resting position · Metafizzy blog](https://metafizzy.co/blog/math-time-resting-position/)

In source of the map engine Leaflet
https://github.com/Leaflet/Leaflet/blob/63fd4edc76893ab2a2f83d54e703e0a4da73de7b/src/map/handler/Map.Drag.js

## Particles

- [gifloopcoder-scripts/roy-dust.js at master · roytanck/gifloopcoder-scripts](https://github.com/roytanck/gifloopcoder-scripts/blob/master/code/roy-dust.js) - Particle emitter [Roy Tanck on Twitter: "Quick & easy TGIF #gifloopcoder GIF. Code (very little of it, actually): https://t.co/Gr4wDVeKLU https://t.co/yUIXacFrBR"](https://twitter.com/roytanck/status/840279090296967168)

## Character control

- [Phase-Functioned Neural Networks for Character Control](http://theorangeduck.com/page/phase-functioned-neural-networks-character-control)
