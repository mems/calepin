- [Humus - Cool](http://www.humus.name/index.php?page=Cool&ID=8) - Particle trimmer: generates an optimized polygon that fully encloses the particle in as tight area as possible given the provided number of vertices allowed
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/diskbbox/diskbbox.htm) - disk and cylinder bounding box
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/ellipses/ellipses.htm) - working with ellipses
- [Inigo Quilez :: fractals, computer graphics, mathematics, demoscene and more](http://www.iquilezles.org/www/articles/sphereocc/sphereocc.htm) - sphere visibility (collision)
 
	// https://www.shadertoy.com/view/MtcXRf
	// Created by inigo quilez - iq/2016
	// License Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported License.
	
	//
	// See http://iquilezles.org/www/articles/diskbbox/diskbbox.htm
	//
	//
	// Analytical computation of the exact bounding box for an arbitrarily oriented disk. 
	// It took me a good two hours to find the symmetries and term cancellations that 
	// simplified the original monster equation into something pretty compact in its final form.
	//
	// For a disk of raius r centerd in the origin oriented in the direction n, has extent e:
	//
	// e = r·sqrt(1-n²)
	//
	// Derivation and more info in the link above
	
	
	#define AA 3
	
	struct bound3
	{
		vec3 mMin;
		vec3 mMax;
	};
	
	//---------------------------------------------------------------------------------------
	// bounding box for a cylinder (http://iquilezles.org/www/articles/diskbbox/diskbbox.htm)
	//---------------------------------------------------------------------------------------
	bound3 CylinderAABB( in vec3 pa, in vec3 pb, in float ra )
	{
		vec3 a = pb - pa;
		vec3 e = ra*sqrt( 1.0 - a*a/dot(a,a) );
	
		return bound3( min( pa - e, pb - e ),
					   max( pa + e, pb + e ) );
	}
	
	// ray-cylinder intersetion (returns t and normal)
	vec4 iCylinder( in vec3 ro, in vec3 rd, 
					in vec3 pa, in vec3 pb, in float ra ) // point a, point b, radius
	{
		// center the cylinder, normalize axis
		vec3 cc = 0.5*(pa+pb);
		float ch = length(pb-pa);
		vec3 ca = (pb-pa)/ch;
		ch *= 0.5;
	
		vec3  oc = ro - cc;
	
		float card = dot(ca,rd);
		float caoc = dot(ca,oc);
	
		float a = 1.0 - card*card;
		float b = dot( oc, rd) - caoc*card;
		float c = dot( oc, oc) - caoc*caoc - ra*ra;
		float h = b*b - a*c;
		if( h<0.0 ) return vec4(-1.0);
		h = sqrt(h);
		float t1 = (-b-h)/a;
		//float t2 = (-b+h)/a; // exit point
	
		float y = caoc + t1*card;
	
		// body
		if( abs(y)<ch ) return vec4( t1, normalize( oc+t1*rd - ca*y ) );
	
		// caps
		float sy = sign(y);
		float tp = (sy*ch - caoc)/card;
		if( abs(b+a*tp)<h )
		{
			return vec4( tp, ca*sy );
		}
	
		return vec4(-1.0);
	}
	
	
	// ray-box intersection
	vec2 iBox( in vec3 ro, in vec3 rd, in vec3 cen, in vec3 rad ) 
	{
		vec3 m = 1.0/rd;
		vec3 n = m*(ro-cen);
		vec3 k = abs(m)*rad;
	
		vec3 t1 = -n - k;
		vec3 t2 = -n + k;
	
		float tN = max( max( t1.x, t1.y ), t1.z );
		float tF = min( min( t2.x, t2.y ), t2.z );
	
		if( tN > tF || tF < 0.0) return vec2(-1.0);
	
		return vec2( tN, tF );
	}
	
	
	float hash1( in vec2 p )
	{
		return fract(sin(dot(p, vec2(12.9898, 78.233)))*43758.5453);
	}
	
	void mainImage( out vec4 fragColor, in vec2 fragCoord )
	{
		vec3 tot = vec3(0.0);
	
	#if AA>1
		for( int m=0; m<AA; m++ )
		for( int n=0; n<AA; n++ )
		{
			// pixel coordinates
			vec2 o = vec2(float(m),float(n)) / float(AA) - 0.5;
			vec2 p = (-iResolution.xy + 2.0*(fragCoord+o))/iResolution.y;
	#else	
			vec2 p = (-iResolution.xy + 2.0*fragCoord)/iResolution.y;
	#endif
	
			// camera position
			vec3 ro = vec3( -0.5, 0.4, 1.5 );
			vec3 ta = vec3( 0.0, 0.0, 0.0 );
			// camera matrix
			vec3 ww = normalize( ta - ro );
			vec3 uu = normalize( cross(ww,vec3(0.0,1.0,0.0) ) );
			vec3 vv = normalize( cross(uu,ww));
			// create view ray
			vec3 rd = normalize( p.x*uu + p.y*vv + 1.5*ww );
	
			// cylidner animation
			vec3  c_a =  0.2 + 0.3*sin(iGlobalTime*vec3(1.11,1.27,1.47)+vec3(2.0,5.0,6.0));
			vec3  c_b = -0.2 + 0.3*sin(iGlobalTime*vec3(1.23,1.41,1.07)+vec3(0.0,1.0,3.0));
			float c_r =  0.3 + 0.2*sin(iGlobalTime*1.3+0.5);
	
	
			// render
			vec3 col = vec3(0.4)*(1.0-0.3*length(p));
	
			// raytrace
			vec4 tnor = iCylinder( ro, rd, c_a, c_b, c_r );
			float t = tnor.x;
			float tmin = 1e10;
			if( t>0.0 )
			{
				tmin = t;
				// shading/lighting	
				vec3 pos = ro + t*rd;
				vec3 nor = tnor.yzw;
				float dif = clamp( dot(nor,vec3(0.5,0.7,0.2)), 0.0, 1.0 );
				float amb = 0.5 + 0.5*dot(nor,vec3(0.0,1.0,0.0));
				col = sqrt( vec3(0.2,0.3,0.4)*amb + vec3(0.8,0.7,0.5)*dif );
				col *= vec3(1.0,0.75,0.3);
			}
	
	
			// compute bounding box of cylinder
			bound3 bbox = CylinderAABB( c_a, c_b, c_r );
	
			// raytrace bounding box
			vec3 bcen = 0.5*(bbox.mMin+bbox.mMax);
			vec3 brad = 0.5*(bbox.mMax-bbox.mMin);
			vec2 tbox = iBox( ro, rd, bcen, brad );
			if( tbox.x>0.0 )
			{
				// back face
				if( tbox.y < tmin )
				{
					vec3 pos = ro + rd*tbox.y;
					vec3 e = smoothstep( brad-0.03, brad-0.02, abs(pos-bcen) );
					float al = 1.0 - (1.0-e.x*e.y)*(1.0-e.y*e.z)*(1.0-e.z*e.x);
					col = mix( col, vec3(0.0), 0.25 + 0.75*al );
				}
				// front face
				if( tbox.x < tmin )
				{
					vec3 pos = ro + rd*tbox.x;
					vec3 e = smoothstep( brad-0.03, brad-0.02, abs(pos-bcen) );
					float al = 1.0 - (1.0-e.x*e.y)*(1.0-e.y*e.z)*(1.0-e.z*e.x);
					col = mix( col, vec3(0.0), 0.15 + 0.85*al );
				}
			}
	
			// no gamma required here, it's done in line 118
	
			tot += col;
	#if AA>1
		}
		tot /= float(AA*AA);
	#endif
	
		// dithering
		tot += ((hash1(fragCoord.xy)+hash1(fragCoord.yx+13.1))/2.0 - 0.5)/256.0;
	
	
		fragColor = vec4( tot, 1.0 );
	}