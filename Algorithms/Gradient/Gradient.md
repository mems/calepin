Gradients in Photoshop: Linear, Reflected, Radial, Diamond, Angle.

Repeat, mirror.

See also [resample](Resample)

- [Gradient — Wikipedia](https://en.wikipedia.org/wiki/Gradient)
- [rectangular gradient · ariya.io](https://ariya.io/2011/06/rectangular-gradient)
- [Gradients](https://bjango.com/articles/gradients/)
- [Gradients and Parametric Curves in Photoshop | Photoshop, etc.](http://www.davidebarranca.com/2013/03/gradients-and-parametric-curves-in-photoshop/)
- [svg multiple color on circle stroke - Stack Overflow](https://stackoverflow.com/questions/18206361/svg-multiple-color-on-circle-stroke)
- [forked from: Delaunay三角分割 - wonderfl build flash online](http://wonderfl.net/c/mDMA/) - Gradient using delaunay
 
	// From http://editor.thebookofshaders.com/?log=170202213311
	#ifdef GL_ES
	precision mediump float;
	#endif
	
	uniform vec2 u_resolution;
	uniform vec2 u_mouse;
	uniform float u_time;
	
	void main() {
	    vec2 st = gl_FragCoord.xy/u_resolution.xy;
	    st.x *= u_resolution.x/u_resolution.y;
	
	    vec3 color = vec3(0.);
	    color = vec3(st.x,st.y,abs(sin(u_time)));
	
	    gl_FragColor = vec4(color,1.0);
	}

## Correct color interpolation

See [correct color interpolation](Interpolation#correct-color-interpolation)

## Angle gradient

Aka conic gradient, conical gradient, whirl, fowler angle

	var bd;//bitmap data 200x200; int() = 32 bit signed int
	var E = 1410;
	for (i = 0; i < 200; i++){
		for (j = 0; j < 200; j++) {
			dx = i - 99.5;
			dy = j - 99.5;
			a1 = 4 + 4 * Math.atan2 (dy, dx) / Math.PI;
			bd.setPixel (i, j + 200, 0x10101 * int ( 32 * a2 ));
		}
	}
		

- [CSS conic-gradient() polyfill](http://leaverou.github.io/conic-gradient/) - draw small triangles for 360° to simulate conical gradient, angle gradient with steps. See [Polyfill for conic-gradient() and repeating-conic-gradient()](https://github.com/LeaVerou/conic-gradient)

## Diamond-square

See [Diamond-square algorithm](Algorithms#diamond-square)

- [labs.hellokeita.com » Multi Gradient](http://wayback.archive.org/web/20120225094220/http://labs.hellokeita.com/2008/01/24/multi-gradient/)

## Plasma effect

See [Sinusoids combination](Random, noise and dithering#sinusoids-combination)

## Scrim gradient

> A scrim is a visual design aid that softens an image so that overlaid text becomes more legible.
— [When Large Isn't Large Enough: Designing With Hero Images – Smashing Magazine](https://www.smashingmagazine.com/2017/06/designing-hero-images/#scrims)

2x length,  (~5 to 9) stops with cubic approximation gradient color

> Center point of gradient: 3/10ths closer the darker end

![Better gradient scrims](Better%20gradient%20scrims%201.png)
![The overall darkness of the 2x-length cubic gradient is similar to the linear gradient, resulting in a similar visual look.](Better%20gradient%20scrims%202.png)

- [Easing Linear Gradients | CSS-Tricks](https://css-tricks.com/easing-linear-gradients/)
- [Imagery - Style - Material design guidelines](https://material.io/guidelines/style/imagery.html#imagery-ui-integration) - See "Text protection"
- [Better gradient scrims While material design tends to discourage the use of ...](https://plus.google.com/+RomanNurik/posts/2QvHVFWrHZf)
- [muzei/ScrimUtil.java at master · romannurik/muzei](https://github.com/romannurik/muzei/blob/master/main/src/main/java/com/google/android/apps/muzei/util/ScrimUtil.java)