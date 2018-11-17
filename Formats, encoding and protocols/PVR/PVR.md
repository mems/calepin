Texture container. Can contains multiple levels (mipmap) encoded with PVRTC, ETC, S3TC/DXT and ATC, BC, etc.

The PVR Container Format

Not to be confused with the PVRTC compression format, the PVR container format describes how the data in a texture file should be interpreted. A PVR file can contain uncompressed data or compressed data in numerous formats (including S3TC, ETC, and PVRTC).

There are a few different, mutually-incompatible versions of the PVR format. This means that each version of PVR requires different code to parse correctly. For example, the header structure for the “legacy” format (PVRv2) looks like this:

Little endian

	// pvrTag = 0x50565221
	struct PVRv2Header
	{
		uint32_t headerLength;
		uint32_t height;
		uint32_t width;
		uint32_t mipmapCount;
		uint32_t flags;
		uint32_t dataLength;
		uint32_t bitsPerPixel;
		uint32_t redBitmask;
		uint32_t greenBitmask;
		uint32_t blueBitmask;
		uint32_t alphaBitmask;
		uint32_t pvrTag;
		uint32_t surfaceCount;
	};

The header structure for the most recent version (PVRv3) looks like this:

	// version = 0x50565203
	struct PVRv3Header {
		uint32_t version;
		uint32_t flags;
		uint64_t pixelFormat;
		uint32_t colorSpace;
		uint32_t channelType;
		uint32_t height;
		uint32_t width;
		uint32_t depth;
		uint32_t surfaceCount;
		uint32_t faceCount;
		uint32_t mipmapCount;
		uint32_t metadataLength;
	};

There are more similarities than differences between the headers. The various fields describe the contained data, including the texture’s dimensions and whether the file contains a set of mipmaps or a single image. If the file contains mipmaps, they are simply concatenated together with no padding. The program reading the file is responsible for calculating the expected length of each image.

Note that the header also has `surfaceCount` and (in the case of PVRv3) `faceCount` fields, which can be used when writing texture arrays or cube maps into a single file.

Note: Valid PVR is at least 32 bytes in size. This means that images that are 8×8 or smaller will be padded to 32 bytes total before being written to the archive. For example, compressing a 4×4 image consumes 32 bytes, even though it only requires 8 bytes of storage.

- [PVR - Vita Dev Wiki](http://www.vitadevwiki.com/index.php?title=PVR)
- v3 [PVR File Format - PVR+File+Format.Specification.pdf](http://cdn.imgtec.com/sdk-documentation/PVR+File+Format.Specification.pdf)
- https://github.com/powervr-graphics/WebGL_SDK/tree/4.0/Documentation
- [PVR Format - IESDP Updates and Info - The Gibberlings Three Forums](http://gibberlings3.net/forums/index.php?showtopic=26065) archive: https://archive.is/http://gibberlings3.net/forums/index.php?showtopic=26065

## Input

See [Texture format](Texture format)

- http://trac.openscenegraph.org/projects/osg//browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osgPlugins/pvr/ReaderWriterPVR.cpp
- https://github.com/powervr-graphics/WebGL_SDK/blob/4.0/Tools/PVRTexture.js
- https://github.com/powervr-graphics/Native_SDK/blob/4.1/Framework/PVRAssets/FileIO/TextureReaderPVR.cpp
- [PvrSharp](https://hg.codeplex.com/pvrsharp), archive: [C# Free Code - Download PvrSharp](http://www.java2s.com/Open-Source/CSharp_Free_Code/Library/Download_PvrSharp.htm)
- https://github.com/sergeyreznik/et-engine/blob/master/src/imaging/pvrloader.cpp
- https://github.com/kexplo/irrlicht_ogl-es/blob/master/source/Irrlicht/CImageLoaderPVR.cpp
- https://github.com/mrdoob/three.js/blob/master/examples/js/loaders/PVRLoader.js
- https://bitbucket.org/sinbad/ogre/commits/9c1b2dd18371/ support PVRv3 instead of PVRv2 (See [Texture format](Texture format))
- https://github.com/cocos2d/cocos2d-objc/blob/develop/cocos2d/CCTexturePVR.m

## Output

See [Texture format](Texture format)

- [Agent_007 / PVRTC encoder/decoder for Unity — Bitbucket](https://bitbucket.org/Agent_007/pvrtc-encoder-decoder-for-unity)
- [jthlim / PvrTcCompressor — Bitbucket](https://bitbucket.org/jthlim/pvrtccompressor)