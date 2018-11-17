- [S3 Texture Compression — Wikipedia](https://en.wikipedia.org/wiki/S3_Texture_Compression)
- [JavaScript implementation of S3TC algorithm](https://github.com/dmikis/S3TC)
- [Texture Compression | RenderingPipeline](http://renderingpipeline.com/2012/07/texture-compression/)
- [Multimedia Formats and Tools - PS3 Developer wiki](http://www.psdevwiki.com/ps3/Multimedia_Formats_and_Tools#DXT)
- [DXT Compression Techniques · Simon's Graphics Blog](http://www.sjbrown.co.uk/2006/01/19/dxt-compression-techniques/)
- [S3 Texture Compression - OpenGL.org](https://www.opengl.org/wiki/S3_Texture_Compression)
- [DXT compression explained - FSDeveloper Wiki](http://www.fsdeveloper.com/wiki/index.php?title=DXT_compression_explained)
- [Texture formats overview - FSDeveloper Wiki](http://www.fsdeveloper.com/wiki/index.php?title=Texture_formats_overview)
- [Legacy:DXT - Unreal Wiki](https://wiki.beyondunreal.com/Legacy:DXT)


S3TC, also known as DXT, was the first compressed format to gain broad adoption, due to its inclusion in DirectX 6.0 and OpenGL 1.3 in 1998 and 2001, respectively

DXT1 normally provides 4 shades of color with no alpha but if the 2 565 colors are reversed, there are 3 colors and transparency.  Transparency is not filtered.  (DXT5 alpha is filtered)

DXT3 is not a "good choice" for "sharp alpha." If alpha is really just on or off, use DXT1, beacuse it's smaller. If alpha is more than that, use DXT5, which approximately always has better quality (3 bit palette between two 8-bit values) than DXT3 (4-bit direct values).

## Variants

RGTC and LATC use DXT but to store two channel only:

- latc: rgba=(x,x,x,y)
- rgtc as rgba=(x,y,0,1)

3DC use DXT compression

ATITC/ATC use a very similar compression

For potential better results

Obviously these format are only supported on GPU that support S3TC/DXT

- [Fast CPU DXT Compression | Intel® Software](https://software.intel.com/en-us/articles/fast-cpu-dxt-compression)
- [Real-Time Normal Map DXT Compression | NVIDIA](http://www.nvidia.com/object/real-time-normal-map-dxt-compression.html)

### YCoCg-DXT Compression

- [Real-Time YCoCg DXT Compression - Real-Time YCoCg-DXT Compression.pdf](http://developer.download.nvidia.com/whitepapers/2007/Real-Time-YCoCg-DXT-Compression/Real-Time%20YCoCg-DXT%20Compression.pdf)
- [High Quality DXT Compression Techniques](https://github.com/castano/nvidia-texture-tools/wiki/HighQualityDXTCompression)

### CRN Crunch format

	 ./crunch -file image.png -fileformat dds -DXT5 -yflip

- [BinomialLLC/crunch- Advanced DXTc texture compression and transcoding library](https://github.com/BinomialLLC/crunch) and https://github.com/BKcore/crunch-osx (patched version that compile on OSX)
- Crunch documentation https://github.com/BinomialLLC/crunch/tree/wiki
- [GDC 2012: DXT is NOT ENOUGH! Advanced texture compression for games - YouTube](https://www.youtube.com/watch?v=7bJ-D1xXEeg)
- [Fun with with Emscripten, Crunch, and DXT: More Info](http://www-cs-students.stanford.edu/~eparker/files/crunch/more_info.html)
- [Rich Geldreich's Tech And Programmer Culture Blog: "Crunch" Open Source Texture Compression Library vs. US Patent #20110115806](http://richg42.blogspot.fr/2012/07/the-saga-of-crunch.html)
- https://github.com/toji/texture-tester/blob/master/js/webgl-texture-util.js at `decompressCRN()`. Use Emscripten-ified version of Crunch decoder See [Texture format](Texture format)

### RGBV format

Aka WayForward's .anb format

Better result than DXT by using an additional channel

This is a variant of RGBM using two DXT1 blocks in order to get free alpha mask

- [RGBV Texture Compression in DuckTales: Remastered](http://files.wayforward.com/shane/rgbv/)
- [Simple image-decompressing program for WayForward's .anb format](https://github.com/meh2481/wfLZEx)
- [Graphic Rants: RGBM color encoding](http://graphicrants.blogspot.fr/2009/04/rgbm-color-encoding.html)

## Input

- https://github.com/pasu/squishjs
- https://github.com/svn2github/libsquish
	* (archive) [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/libsquish/)
	* (other potential clones and forks) https://github.com/search?utf8=%E2%9C%93&q=squish&type=Repositories&ref=searchresults
	* (other potential clones and forks) https://github.com/search?utf8=%E2%9C%93&q=libsquish&type=Repositories&ref=searchresults
- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osgPlugins/dds/ReaderWriterDDS.cpp

## Output

See [Texture format](Texture format)

	convert image_rgba.png -format dds -define dds:compression=dxt5 -define dds:cluster-fit=true -define dds:mipmaps=0 image_rgba_dxt5.dds

- [FastDXT](https://www.evl.uic.edu/cavern/fastdxt/), https://www.evl.uic.edu/cavern/fastdxt/dl/FastDXT.zip
- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osg/dxtctool.h?rev=12598
- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osg/dxtctool.cpp?rev=12598
- [Download DirectX Software Development Kit from Official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=6812) (DirectXTex) BC1 – BC7
- [DXT Compression - Retired | Intel® Software](https://software.intel.com/en-us/articles/dxt-compression-sample) http://software.intel.com/sites/products/vcsource/files/45662/DXTCompressor.zip