Often used by light devices like smartphones or tablets with PowerVR chipsets (Apple iPhone, iPad) and some Android devices

- PVRTC 2bpp (v1) (RGB)
- PVRTC 2bpp (v1) (RGBA)
- PVRTC 4bpp (v1) (RGB)
- PVRTC 4bpp (v1) (RGBA)

On iOS: Must be square (height==width) and be a power of 2

- [PVRTC — Wikipedia](https://en.wikipedia.org/wiki/PVRTC)
- [PVRTC: the most efficient texture compression standard for the mobile graphics world - With Imagination](https://imgtec.com/blog/pvrtc-the-most-efficient-texture-compression-standard-for-the-mobile-graphics-world/)
- [PVRTC2 – taking texture compression to a new dimension - With Imagination](https://imgtec.com/blog/pvrtc2-taking-texture-compression-to-a-new-dimension/)
- https://github.com/powervr-graphics/WebGL_SDK/tree/4.0/Documentation
- [PVR Format - IESDP Updates and Info - The Gibberlings Three Forums](http://gibberlings3.net/forums/index.php?showtopic=26065) archive: https://archive.is/http://gibberlings3.net/forums/index.php?showtopic=26065
- [PVR Texture Compression Exploration](http://roartindon.blogspot.fr/2014/08/pvr-texture-compression-exploration.html)

How to generate 4bpp and 2bpp data:

- [Texture Compression using Low-Frequency Signal Modulation](http://web.onetel.net.uk/~simonnihal/assorted3d/fenney03texcomp.pdf)
- [Fast PVRTC Texture Compression using Intensity Dilation](http://jcgt.org/published/0003/04/07/paper-lowres.pdf)

Note: Only square (power-of-two) dimension textures are determined to work consistently, although in some cases, rectangular support is provided for the compressed texture
Note: The PVRTC header is packed due to the presence of the 64-bit pixel format data member (mPixelFormat in the sample). ARM attempts to align the header by padding it with 4 additional bytes, making the header a total of 56 bytes instead of the raw 52 bytes. This in turn causes the image to be distorted when displayed on an ARM device. Intel devices do not pad the header, and so isn’t an issue. Packing the header solves the ARM padding issue, and the texture displays correctly on both ARM and Intel devices.
"Intel devices do not pad the header": it's not the devices that do the padding, it's the compier. By default, compilers for Intel CPUs pad to natural/4-byte, and the ARM compiler pads for natural/8-byte. It's compiler options, not device specifics, that affect structure layout in memory.

## Input

- https://github.com/tlozoot/decompress-pvrtc/blob/master/fortseige_pvr.c
- [Agent_007 / PVRTC encoder/decoder for Unity — Bitbucket](https://bitbucket.org/Agent_007/pvrtc-encoder-decoder-for-unity)
- [jthlim / PvrTcCompressor — Bitbucket](https://bitbucket.org/jthlim/pvrtccompressor)
- [PvrSharp](https://hg.codeplex.com/pvrsharp) see [PVR](PVR)
- https://bitbucket.org/sinbad/ogre/src/default/OgreMain/src/OgrePVRTCCodec.cpp
- https://github.com/ftrvxmtrx/erszebet/blob/master/src/image/image_pvrtc.c

## Output

See [Texture format](Texture format)

- [Agent_007 / PVRTC encoder/decoder for Unity — Bitbucket](https://bitbucket.org/Agent_007/pvrtc-encoder-decoder-for-unity)
- [jthlim / PvrTcCompressor — Bitbucket](https://bitbucket.org/jthlim/pvrtccompressor)