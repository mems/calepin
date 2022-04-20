See also [S3TC - DXT](../S3TC%20-%20DXT/S3TC%20-%20DXT.md), [PVRTC](../PVRTC/PVRTC.md), [PVR](../PVR/PVR.md), [OpenGL - DX3D API Proxies](../../Graphics/3D%20-%20GPU/OpenGL%20-%20DX3D%20API%20Proxies), [KTX](../KTX/KTX.md), [ETC](../ETC/ETC.md), [DDS](../DDS/DDS.md)

Infos:

- [OpenGL ES | Android Developers](https://developer.android.com/guide/topics/graphics/opengl.html#textures)
- [OpenGL® Registry](https://www.opengl.org/registry/)
- [\<supports-gl-texture\> | Android Developers](https://developer.android.com/guide/topics/manifest/supports-gl-texture-element.html)
- [Best Practices for Working with Texture Data](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/TechniquesForWorkingWithTextureData/TechniquesForWorkingWithTextureData.html#//apple_ref/doc/uid/TP40008793-CH104-SW1)

Aditional compression can be applied:

- lossless [JPEG XR](https://en.wikipedia.org/wiki/JPEG_XR#Compression_algorithm) compression
- LZMA/deflate
- Generalized Texture Compression (See [GST](GST))

[ATF](#atf) use this technique

## Premultiplied alpha

To premultiply alpha (for formats that don't use it) of an PNG image:

```sh
convert RGBA.png \( +clone -alpha Extract \) -channel RGB -compose Multiply -composite RGBA_premultiplied.png
```

See also:

- [Premultiplied alpha](../../Graphics/Graphics.md#premultiplied-alpha)

## Optimizations

Reduce artifacts

- super sampling (then downscale like *0.5)
- add noise post-processing (shader, blend with an other texture)
- bleed edges
	See also alpha bleeding
	- [Adding bleed margins to CSS sprites with ImageMagick - Super User](http://superuser.com/questions/755134/adding-bleed-margins-to-css-sprites-with-imagemagick)
- alpha bleeding: adds color to transparent pixels of adjacent opaque pixels by repeating a sprite's outer color values (like bleed edges, but only for RGB channels)
	See also bleed edges and [Color bleed](../../Graphics/Color%20bleed/Color%20bleed.md).

	Happend when textures when transform is applyed (scale, rotation, perspective).

	Remove white/dark outlines/borders/halos/fringing.

	Defringe / dilate RGB
	These color values can reduce artifacts around sprites and removes dark halos at transparent borders. This feature is also known as "Alpha bleeding".
	This only works only when the alpha is not pre-multiplied (aka premultiplied alpha), `glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);` it will produce black outlines
	The mipmapping and filtering can (blend between pixels) can cause this problem
	See [TexturePacker Online Documentation](https://www.codeandweb.com/texturepacker/documentation)
	Should be aligned to few blocks (texture compression blocks) aways
	Fully transparent pixels are often filled with `rgba(1.0, 1.0, 1.0, 0.0)`

	- [Unity - Manual: How do I Import Alpha Textures?](https://docs.unity3d.com/Manual/HOWTO-alphamaps.html) and `AlphaUtility.atn`
	- [PNG transparency has white border/halo - Unity Answers](http://answers.unity3d.com/questions/238922/png-transparency-has-white-borderhalo.html#answer-949217)
	- [Messy Alpha Problem - White around edges - Unity Answers](http://answers.unity3d.com/questions/10302/messy-alpha-problem-white-around-edges.html)
	- [OpenGL filters and Sprite bleeding | J Fixby](https://jfixbi.wordpress.com/2013/02/23/opengl-filters/)
	- [Scaling images with alpha - Wolfire Games Blog](http://blog.wolfire.com/2009/01/scaling-images-with-alpha/)
- clean transparent pixels (outside alpha bleeding)
- align to compression blocks
- use [dithering](../../Algorithms/Random,%20noise%20and%20dithering/Random,%20noise%20and%20dithering.md#dithering):
	Add noise pre-processing (before compression) depends algorithm used to compress (especially for gradient with PVRTC1). See [Making the quality of PVRTC textures higher | Heyworks Blog](http://wayback.archive.org/web/20160406130348/http://blog.heyworks.com/making-the-quality-of-pvrtc-textures-higher/) or [Избавление от артефактов сжатия PVRTC текстур / Хабрахабр](https://habrahabr.ru/post/158963/)

	- nearest-neighbour, has the least color error but color distribution leads to less contrast than linear.
	- linear color distribution with some color error but better contrast than nearest-neighbour.
	- Floyd-Steinberg
	- Floyd-Steinberg with alpha values.
	- Atkinson
	- Atkinson with alpha values.
- use channel swizzle (require shader when it's not supported): [Texture swizzling in OpenGL, OpenGL ES and WebGL](https://www.g-truc.net/post-0734.html)
	Add more precision to defined channels

	- https://www.opengl.org/wiki/Texture#Swizzle_mask
- [How to get the best out of PVRTC for iOS - Kruger Heavy Industries Devlog](http://www.krugerheavyindustries.com/pebble/2012/04/02/1333338720000.html)
- [Dimensionality reduction for image and texture set compression | Bart Wronski](https://bartwronski.com/2020/05/21/dimensionality-reduction-for-image-and-texture-set-compression/) - Use multiple channels to compress PBR textures, an experiment

Use [Chroma subsampling](https://en.wikipedia.org/wiki/Chroma_subsampling) like [YCbCr](https://en.wikipedia.org/wiki/YCbCr) (like JPEG) or [YCgCo](https://en.wikipedia.org/wiki/YCgCo) (like YCoCg DXT5)
Need a custom shader
http://www.pmavridis.com/research/wavelet_texture_compression/PG2012_WaveletTC_Preprint.pdf
- https://github.com/n-yoda/unity-ycca-subsampling
- https://github.com/keijiro/ChromaPack

## Formats

Containers: DDS, PVR, KTX, PKM (no mipmap)
Codecs: S3TC/DXT (DXT1, DXT2), PVRTC, ATITC/ATC, ETC1, BPTC (BC7), ASTC, 3DC, RGTC1 (BC4), etc.

Specific: Crabby, S3TC/DXT derivated (RGBV, RGBM, CRN, YCoCg DXT5)

- KTX, an OpenGL standard, multiple mipmap levels supported with multitude of texture formats.
- PKM, for ETC textures containing a single mipmap level.
- DDS, for DXTC, RGTC, BPTC (BC1-7) or uncompressed textures, multiple mipmap levels supported.
- PKM is a simple file format for single compressed images. If you generate mipmaps, multiple PKM files are created.
- KTX format that provides a container for images. If you generate mipmaps, a single KTX file is generated.

Block Compression:

| FOURCC | DX Name | Bit/channel | Description          | Alpha premultiplied? | Compression ratio            | Texture Type     |
|--------|---------|-------------|----------------------|----------------------|------------------------------|------------------|
| DXT1   | BC1     |             | 1-bit Alpha / Opaque | Yes                  | 6:1(for 24 bit source image) | Simple non-alpha |
| DXT2   | BC2     |             | Explicit alpha       | Yes                  | 4:1                          | Sharp alpha      |
| DXT3   | BC2     |             | Explicit alpha       | No                   | 4:1                          | Sharp alpha      |
| DXT4   | BC3     |             | Interpolated alpha   | Yes                  | 4:1                          | Gradient alpha   |
| DXT5   | BC3     |             | Interpolated alpha   | No                   | 4:1                          | Gradient alpha   |

| Name | FourCC | DX name | Channels                   | Data Rate | Palette Size      | Line Segments     | Use For                                                                     |
|------|--------|---------|----------------------------|-----------|-------------------|-------------------|-----------------------------------------------------------------------------|
| BC1  | DXT1   | BC1     | RGB + optional 1-bit alpha | 4 bit/px  | 4                 | 1                 | Color maps Cutout color maps (1-bit alpha), Normal maps, if memory is tight |
| BC2  | DXT2-3 | BC2     | RGB + 4-bit alpha          | 8 bit/px  | 4                 | 1                 | n/a                                                                         |
| BC3  | DXT4-5 | BC3     | RGBA                       | 8 bit/px  | 4 color + 8 alpha | 1 color + 1 alpha | Color maps with full alpha, Packing color and mono maps together            |
| BC4  |        | BC4     | Grayscale                  | 4 bit/px  | 8                 | 1                 | Height maps, Gloss maps, Font atlases, Any grayscale image                  |
| BC5  |        | BC5     | 2 × grayscale              | 8 bit/px  | 8 per channel     |                   | 1 per channel                                                               |
| BC6  |        | BC6     | RGB, floating-point        | 8 bit/px  | 8–16              | 1–2               | HDR images                                                                  |
| BC7  |        | BC7     | RGB or RGBA                | 8 bit/px  | 4–16              | 1–3               | High-quality color maps, Color maps with full alpha                         |

- [Block Compression (Direct3D 10) (Windows)](https://msdn.microsoft.com/en-us/library/bb694531.aspx)
- [Texture Block Compression in Direct3D 11 (Windows)](https://msdn.microsoft.com/en-us/library/hh308955.aspx)
- [Using ASTC Texture Compression for Game Assets | NVIDIA Developer](https://developer.nvidia.com/astc-texture-compression-for-game-assets)
- [ETC1 Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#ETC1)
- [ETC2 Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#ETC2)
- [S3TC Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#S3TC)
- [RGTC Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#RGTC)
- [BPTC Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#BPTC)
- [ASTC Compressed Texture Image Formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#ASTC)

- [Understanding BCn Texture Compression Formats – Nathan Reed’s coding blog](http://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/)
- [Texture Block Compression in Direct3D 11 (Windows)](https://msdn.microsoft.com/en-us/library/windows/desktop/hh308955%28v=vs.85%29.aspx)
- [DirectX Compressed VolumeTexture Formats (Windows Drivers)](https://msdn.microsoft.com/en-us/library/windows/hardware/ff553847(v=vs.85).aspx)
- [BPTC Texture Compression - OpenGL.org](https://www.opengl.org/wiki/BPTC_Texture_Compression)
- [Red Green Texture Compression - OpenGL.org](https://www.opengl.org/wiki/Red_Green_Texture_Compression)
- [3Dc — Wikipedia](https://en.wikipedia.org/wiki/3Dc)
- [Legacy:Texture Format - Unreal Wiki](https://wiki.beyondunreal.com/Legacy:Texture_Format)

- [Gamasutra: Alexandru Voica's Blog - Why efficiency is key in texture compression standards for mobile graphics](http://www.gamasutra.com/blogs/AlexandruVoica/20130419/190833/Why_efficiency_is_key_in_texture_compression_standards_for_mobile_graphics.php)
- [Patent US5585944 - Method for compressing and decompressing images by subdividing pixel color ... - Google Patents](https://www.google.com/patents/US5585944)
- [MOTODEV \> Documentation & Tools > Android Technical Library > Understanding Texture Compression](http://wayback.archive.org/web/20110214195728/http://developer.motorola.com/docstools/library/understanding-texture-compression/)
- [Image Format - OpenGL.org](https://www.opengl.org/wiki/Image_Format#Compressed_formats)
- [Android* Texture Compression - a comparison study with code sample | Intel® Software](https://software.intel.com/en-us/articles/android-texture-compression-a-comparison-study-with-code-sample)
- [Understanding BCn Texture Compression Formats – Nathan Reed’s coding blog](http://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/)
- [Texture compression — Wikipedia](https://en.wikipedia.org/wiki/Texture_compression)
- [FourCC — Wikipedia](https://en.wikipedia.org/wiki/FourCC)

> - Vulkan is based on Mantle and usable on "OpenGL 4.x / OpenGL ES3.1" compatible hardware.
> - Mantle 1.0 has in core[^1] : BC1/DXT1, BC2/DXT3, BC3/DXT5, BC4/ATI1/3Dc+/RGTC1, BC5/ATI2/3Dc/DXN/RGTC2, BC6 and BC7/BPTC.
> - OpenGL 4.3 has in core: ETC2/EAC, RGTC/BC4&5 and BPTC/BC6&7, plus extensions for S3TC/BC1&2&3, and other proprietary formats.
> - OpenGL ES 3.1 has in core: ETC2/EAC, plus extensions for PVRTC, ASTC, and other proprietary formats.
> - WebGL 1.0 has no compressed formats in core, plus an extension for S3TC/BC1&2&3 (plus pending ratifications for ATC/BC4&5, ETC1 and PVRTC, plus drafts for ETC2/EAC and ASTC).
> - Less than 2 years before S3 patent expiration for S3TC/BC1&2&3.
>
> [^1]: There is no reference to whether some compressed format where optional, but the last phrase before listing 9 seems to imply that all Mantle devices support "read-only access of optimally tiled images" for all BCn formats.
— [Some compressed texture formats in "core"? : vulkan](https://www.reddit.com/r/vulkan/comments/3xvl3m/some_compressed_texture_formats_in_core/)

Official texture compression OpenGL extensions:

- https://www.opengl.org/registry/specs/ARB/texture_compression_rgtc.txt
- https://www.opengl.org/registry/specs/KHR/texture_compression_astc_hdr.txt
- https://www.opengl.org/registry/specs/KHR/texture_compression_astc_sliced_3d.txt
- https://www.opengl.org/registry/specs/EXT/texture_compression_s3tc.txt
- https://www.opengl.org/registry/specs/3DFX/texture_compression_FXT1.txt
- https://www.opengl.org/registry/specs/NV/texture_compression_vtc.txt
- https://www.opengl.org/registry/specs/EXT/texture_compression_dxt1.txt
- https://www.opengl.org/registry/specs/EXT/texture_compression_latc.txt
- https://www.opengl.org/registry/specs/EXT/texture_compression_rgtc.txt
- https://www.opengl.org/registry/specs/ARB/texture_compression.txt
- https://www.opengl.org/registry/specs/ARB/texture_compression_bptc.txt
- https://www.khronos.org/registry/gles/extensions/OES/OES_texture_compression_astc.txt

- [DXGI_FORMAT enumeration (Windows)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb173059%28v=vs.85%29.aspx)

---

- explicit, interpolated alpha [Textures with Alpha Channels (Direct3D 9) (Windows)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb206238%28v=vs.85%29.aspx)
	Interpolated alpha: Three bits are used to determine explicit alpha values, and two eight-bit values are used to interpolate gradually between them. This makes the format especially suited for soft gradients and other textures where the alpha areas vary less wildly.
- punchthrough alpha = 0 or 1 (2 values only)
- swizzling [Swizzling (computer graphics) — Wikipedia](https://en.wikipedia.org/wiki/Swizzling_%28computer_graphics%29)

sRGB colorspace and S3TC [S3 Texture Compression - OpenGL.org](https://www.opengl.org/wiki/S3_Texture_Compression#sRGB_and_S3TC)

> ````
> SNORM	Signed normalized integer, meaning that for an n-bit 2's complement number, the maximum value means 1.0f (e.g. the 5-bit value 01111 maps to 1.0f), and the minimum value means -1.0f (e.g. the 5-bit value 10000 maps to -1.0f). In addition, the second-minimum number maps to -1.0f (e.g. the 5-bit value 10001 maps to -1.0f). There are thus two integer representations for -1.0f. There is a single representation for 0.0f, and a single representation for 1.0f. This results in a set of integer representations for evenly spaced floating point values in the range (-1.0f...0.0f), and also a complementary set of representations for numbers in the range (0.0f...1.0f)
> UNORM	Unsigned normalized integer, meaning that for an n-bit number, all 0's means 0.0f, and all 1's means 1.0f. A sequence of evenly spaced floating point values from 0.0f to 1.0f are represented. e.g. a 2-bit UNORM represents 0.0f, 1/3, 2/3, and 1.0f.
> SRGB	Similar to UNORM, in that for an n-bit number, all 0's means 0.0f and all 1's means 1.0f. However unlike UNORM, with SRGB the sequence of unsigned integer encodings between all 0's to all 1's represent a nonlinear progression in the floating point interpretation of the numbers, between 0.0f to 1.0f. Roughly, if this nonlinear progression, SRGB, is displayed as a sequence of colors, it would appear as a linear ramp of luminosity levels to an "average" observer, under "average" viewing conditions, on an "average" display. For complete detail, refer to the SRGB color standard, IEC 61996-2-1, at IEC (International Electrotechnical Commission).
> ````
>
> - [Data Conversion Rules - Windows applications | Microsoft Docs](https://docs.microsoft.com/fr-fr/windows/desktop/direct3d10/d3d10-graphics-programming-guide-resources-data-conversion)

Fixed channels or float channels

Notes:

- DXT1a and DXT1c are the same format (DXT1), just an internal switch for enabling alpha or not
- a FourCC exit in DDS `DX10` used as an DDS header extension: [DDS_HEADER_DXT10 structure (Windows)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb943983%28v=vs.85%29.aspx)

> 3Dc format is an other version of RGTC/BC5
> VTC is NVidia's application of this same base compression method (DXT/S3TC) to 3D textures IIRC
> BPTC extension/formats offers higher quality LDR compression and HDR compression (it's a modified DXT)

**The following tables contains (lot of) duplicates:**

| Name                                 | FourCC | DX name | Channels | Depth (bit/channel) | rate (bit/px) | Alpha                                                    | Comment                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|--------------------------------------|--------|---------|----------|---------------------|---------------|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| S3TC DXT1/DXT1c                      | BC1    | BC1     | RGB      | 5:6:5               | 4             | N/A                                                      | Useful for color maps or normal maps if memory is tight. Generally the best DXT format for textures without an Alpha channel. Doesn't work very well on images that have stark color changes, like pixel art.                                                                                                                                                                                                                                               |
| S3TC DXT1/DXT1c                      | BC1    | BC1     | RGB      | 5:6:5 sRGB          | 4             | N/A                                                      | Same as above with sRGB extended header only on DX10+ level hardware. Generally the best DXT format for textures without an Alpha channel. Doesn't work very well on images that have stark color changes, like pixel art.                                                                                                                                                                                                                                  |
| S3TC DXT1/DXT1a                      | BC1    | BC1     | RGBA     | 5:6:5:1 UNORM       | 4             | explicit                                                 | Generally the best DXT format for textures with just black and white in the Alpha channel, no grays. Doesn't work very well on images that have stark color changes, like pixel art.                                                                                                                                                                                                                                                                        |
| S3TC DXT1/DXT1a                      | BC1    | BC1     | RGBA     | 5:6:5:1 sRGB        | 4             | explicit                                                 | Generally the best DXT format for textures with just black and white in the Alpha channel, no grays. Doesn't work very well on images that have stark color changes, like pixel art.                                                                                                                                                                                                                                                                        |
| S3TC DXT2                            | BC2    | BC2     | RGBA     | 5:6:5:4 UNORM       | 8             | explicit, premultiplied                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT2                            | BC2    | BC2     | RGBA     | 5:6:5:4 sRGB        | 8             | explicit, premultiplied                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT3                            | BC2    | BC2     | RGBA     | 5:6:5:4             | 8             | explicit                                                 | A DXT3-compressed image in an RGBA image format. Compared to a 32-bit RGBA texture, it offers 4:1 compression.                                                                                                                                                                                                                                                                                                                                              |
| S3TC DXT4                            | BC3    | BC3     | RGBA     | 5:6:5:8             | 8             | interpolated, premultiplied                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT5                            | BC3    | BC3     | RGBA     | ?                   | 8             | interpolated                                             | A DXT5-compressed image in an RGBA image format. It also provides a 4:1 compression, but differs to the DXT3 compression in how the alpha compression is done.                                                                                                                                                                                                                                                                                              |
| S3TC DXT5                            | BC3    | BC3     | RGBA     | 5:6:5:8             | 8             | interpolated                                             | Useful for color maps with full alpha, packing color and mono maps together. Contains RGBA types of data.                                                                                                                                                                                                                                                                                                                                                   |
| S3TC DXT5                            | BC3    | BC3     | RGBA     | sRGBA               | 8             | interpolated                                             | Same as above with sRGB extended header only on DX10 + level hardware                                                                                                                                                                                                                                                                                                                                                                                       |
| S3TC DXT1                            | BC1    | BC1     | RGBA     | ?                   | 4             | ?                                                        | Four component opaque (or 1-bit alpha) compressed texture format                                                                                                                                                                                                                                                                                                                                                                                            |
| S3TC DXT2/DXT3                       | BC2    | BC2     | RGBA     | ?                   | 4             | ?                                                        | Four component compressed texture format with explicit alpha                                                                                                                                                                                                                                                                                                                                                                                                |
| S3TC DXT4/DXT5                       | BC3    | BC3     | RGBA     | ?                   | 4             | ?                                                        | Four component compressed texture format with interpolated alpha                                                                                                                                                                                                                                                                                                                                                                                            |
| S3TC DXT5                            | xGBR   | ?       | xGBR     | ?                   | 8             | interpolated                                             | DXT5 with the red component swizzled into the alpha channel                                                                                                                                                                                                                                                                                                                                                                                                 |
| S3TC DXT5                            | RxBG   | ?       | RxBG     | ?                   | 8             | interpolated                                             | Swizzled DXT5 format with the green component swizzled into the alpha channel                                                                                                                                                                                                                                                                                                                                                                               |
| S3TC DXT5                            | RBxG   | ?       | RBxG     | ?                   | 8             | interpolated                                             | Swizzled DXT5 format with the green component swizzled into the alpha channel & the blue component swizzled into the green channel                                                                                                                                                                                                                                                                                                                          |
| S3TC DXT5                            | xRBG   | ?       | xRBG     | ?                   | 8             | interpolated                                             | Swizzled DXT5 format with the green component swizzled into the alpha channel & the red component swizzled into the green channel                                                                                                                                                                                                                                                                                                                           |
| S3TC DXT5                            | RGxB   | ?       | RGxB     | ?                   | 8             | interpolated                                             | Swizzled DXT5 format with the blue component swizzled into the alpha channel                                                                                                                                                                                                                                                                                                                                                                                |
| S3TC DXT5                            | xGxR   | ?       | xGxR     | ?                   | 8             | interpolated                                             | Two-component swizzled DXT5 format with the red component swizzled into the alpha channel & the green component in the green channel                                                                                                                                                                                                                                                                                                                        |
| S3TC DXT5                            | GxRB   | ?       | ?        | ?                   | 8             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT5                            | GRxB   | ?       | ?        | ?                   | 8             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT5                            | RxGB   | ?       | ?        | ?                   | 8             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT5                            | BRGx   | ?       | ?        | ?                   | 8             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| S3TC DXT2                            | ?      | BC2     | ?        | ?                   | 8             | explicit                                                 | Same format as DXT3, except it assumes the alpha is not pre-multiplied. Rarely used because it requires extra processing in the shader.                                                                                                                                                                                                                                                                                                                     |
| S3TC DXT3                            | ?      | BC2     | ?        | :::4                | 8             | ?                                                        | Generally the best DXT format for textures with a sharp Alpha channel. This works well if the alpha values are mostly black and mostly white, with thin anti-aliasing between them. Color is compressed the same as DXT1.                                                                                                                                                                                                                                   |
| S3TC DXT4                            | ?      | BC3     | ?        | ?                   | 8             | ?                                                        | Same format as DXT5, except it assumes the alpha is not pre-multiplied. Rarely used because it requires extra processing in the shader.                                                                                                                                                                                                                                                                                                                     |
| S3TC DXT5                            | ?      | BC3     | ?        | ?                   | 8             | interpolated, premultiplied                              | Generally the best DXT format for textures with a smooth Alpha channel. Color is compressed the same as DXT1. In the alpha channel, each 4x4 block is compressed separately from the others. Two of the pixels are stored in 256 levels of gray, while the other 14 pixels in the block are interpolated between those two, using 8 levels of gray. This works well when each block has a fairly smooth gradation of values, rather than sharp transitions. |
| PVRTC1                               | ?      | ?       | RGB      | ?                   | 4             | N/A                                                      | One block for each 4×4 pixels                                                                                                                                                                                                                                                                                                                                                                                                                               |
| PVRTC1                               | ?      | ?       | RGBA     | ?                   | 4             | ?                                                        | One block for each 4×4 pixels                                                                                                                                                                                                                                                                                                                                                                                                                               |
| PVRTC1                               | ?      | ?       | RGB      | ?                   | 2             | N/A                                                      | One block for each 8×4 pixels                                                                                                                                                                                                                                                                                                                                                                                                                               |
| PVRTC1                               | ?      | ?       | RGBA     | ?                   | 2             | ?                                                        | One block for each 8×4 pixels                                                                                                                                                                                                                                                                                                                                                                                                                               |
| PVRTC2                               | ?      | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| PVRTC                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | The PVRTC image format was introduced by Imagination Technologies, creators of the PowerVR series of GPUs at the heart of every iOS device. It was first described in a 2003 paper by Simon Fenney.                                                                                                                                                                                                                                                         |
| PVRTC                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | operates by downsampling the source image into two smaller images, which are upscaled and blended to reconstruct an approximation of the original. It considers blocks of 4×4 or 4×8 pixels at a time, which are packed into one 64-bit quantity. Thus, each pixel occupies 4 bits or 2 bits, respectively.                                                                                                                                                 |
| PVRTC                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | One significant limitation of using PVRTC format on iOS is that textures must be square, and each dimension must be a power of two. Fortunately, game textures are most commonly produced in dimensions that are compatible with this limitation.                                                                                                                                                                                                           |
| ETC/ETC1                             | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Mandatory in OpenGL 2.0 and OpenGL ES 2.0 and optional in WebGL 1.0                                                                                                                                                                                                                                                                                                                                                                                         |
| ETC2 and EAC                         | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Mandatory in OpenGL 3.0 and OpenGL ES 3.0                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ETC1                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Compatible with OpenGL ES 1.1 and higher.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ETC2                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Highest quality for OpenGL ES 3.0, but not backward (ETC1) compatible.                                                                                                                                                                                                                                                                                                                                                                                      |
| ETC2                                 | ?      | ?       | RGB      | 8:8:8               | ?             | N/A                                                      | Compress RBG8 data with no alpha channel.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:1             | ?             | ?                                                        | This format is very similar to ETC2(RGB8), but has the ability to represent punchthrough alpha, which is the ability to make it completely opaque or transparent.                                                                                                                                                                                                                                                                                           |
| ETC2                                 | ?      | ?       | RGB      | 8:8:8 UNORM         | ?             | N/A                                                      | RGB                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ETC2                                 | ?      | ?       | RGB      | 8:8:8 SRGB          | ?             | N/A                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:1 UNORM       | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:1 SRGB        | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:8 UNORM       | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:8 SRGB        | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2/ETC2_EAC                        | ?      | ?       | RGBA     | 8:8:8:8             | ?             | ?                                                        | Encodes RGBA8 data. The RGB part is encoded the same as ETC2(RGB), but the alpha part is encoded separately.                                                                                                                                                                                                                                                                                                                                                |
| ETC2/EAC                             | ?      | ?       | R        | 11                  | ?             | N/A                                                      | One-channel (red) unsigned format. It is similar to the alpha part of ETC2_EAC(RGB8) but delivers higher precision.                                                                                                                                                                                                                                                                                                                                         |
| ETC                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | debuted in 2005. Similarly to PVRTC’s 4-bit-per-pixel mode, it compresses each 4×4 block of pixels into a single 64-bit quantity, but lacks support for an alpha channel. A subsequent version, ETC2, adds support for 1-bit and 8-bit alpha channels. ETC2 is supported by all Metal-compatible hardware, but PVRTC often offers better quality at comparable file sizes.                                                                                  |
| ETC                                  | ?      | ?       | RGB      | ?                   | ?             | N/A                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC2                                 | ?      | ?       | RGB      | ?                   | ?             | N/A                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC1                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | the mobile standard and compatible with the new standardized ETC2 format in OpenGL 4.3 and OpenGL ES 3.0.                                                                                                                                                                                                                                                                                                                                                   |
| ETC2                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | an improved version of ETC1. RGB8 as well as RGBA8 and RGB8 with punchthrough alpha are supported.                                                                                                                                                                                                                                                                                                                                                          |
| ETC2                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Preliminary support for one or two component textures (stored as one or two 16-bit values in an image file): R11_EAC and RG11_EAC and their signed variants. These are part of the ETC2 family.                                                                                                                                                                                                                                                             |
| ETC1                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | ETC1, an RGB8 format. 64-bit per block (4x4 pixels).                                                                                                                                                                                                                                                                                                                                                                                                        |
| ETC2 RGB8                            | ?      | ?       | ?        | ?                   | ?             | ?                                                        | ETC2 RGB8 format that is backwards compatible with ETC1. 64-bit.                                                                                                                                                                                                                                                                                                                                                                                            |
| ETC2 EAC                             | ?      | ?       | ?        | ?                   | ?             | ?                                                        | ETC2 RGBA8 format with alpha values ranging from 0 to 255. 128-bit blocks.                                                                                                                                                                                                                                                                                                                                                                                  |
| ETC2_PUNCHTHROUGH                    | ?      | ?       | ?        | ?                   | ?             | ?                                                        | RGB8 + alpha that is either on or off (0 or 255). 64-bit blocks.                                                                                                                                                                                                                                                                                                                                                                                            |
| ETC2_RGB                             | ETC2   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ECT EAC                              | ?      | ?       | R        | 11                  | ?             | N/A                                                      | One-channel (red) unsigned format compression.                                                                                                                                                                                                                                                                                                                                                                                                              |
| ECT EAC                              | ?      | ?       | R        | 11 SIGNED           | ?             | N/A                                                      | One-channel (red) signed format compression.                                                                                                                                                                                                                                                                                                                                                                                                                |
| ECT EAC                              | ?      | ?       | RG       | 11:11               | ?             | N/A                                                      | Two-channel (red and green) unsigned format compression.                                                                                                                                                                                                                                                                                                                                                                                                    |
| ECT EAC                              | ?      | ?       | RG       | 11:11 SIGNED        | ?             | N/A                                                      | Two-channel (red and green) signed format compression.                                                                                                                                                                                                                                                                                                                                                                                                      |
| ETC2                                 | ?      | ?       | RGB      | 8:8:8               | ?             | N/A                                                      | Compresses RGB8 data with no alpha channel.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ETC2 EAC                             | ?      | ?       | RGBA     | 8:8:8:8             | ?             | ?                                                        | Compresses RGBA8 data. The RGB part is encoded the same as RGB_ETC2, but the alpha part is encoded separately.                                                                                                                                                                                                                                                                                                                                              |
| ETC2                                 | ?      | ?       | RGB      | 8:8:8 SRGB          | ?             | N/A                                                      | Compresses sRGB8 data with no alpha channel.                                                                                                                                                                                                                                                                                                                                                                                                                |
| ETC2 EAC                             | ?      | ?       | RGBA     | 8:8:8 SRGB + 8      | ?             | ?                                                        | Compresses sRGBA8 data. The sRGB part is encoded the same as SRGB_ETC2, but the alpha part is encoded separately.                                                                                                                                                                                                                                                                                                                                           |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:1             | ?             | ?                                                        | Similar to RGB8_ETC, but with ability to punch through the alpha channel, which means to make it completely opaque or transparent.                                                                                                                                                                                                                                                                                                                          |
| ETC2                                 | ?      | ?       | RGBA     | 8:8:8:1 SRGB        | ?             | ?                                                        | Similar to SRGB8_ETC, but with ability to punch through the alpha channel, which means to make it completely opaque or transparent.                                                                                                                                                                                                                                                                                                                         |
| ETC1                                 | ?      | ?       | RGB      | ?                   | ?             | N/A                                                      | Compresses 24-bit RGB data with no alpha channel.                                                                                                                                                                                                                                                                                                                                                                                                           |
| ETC                                  | ?      | ?       | RGB      | ?                   | ?             | N/A                                                      | Ericsson Texture Compression - Compressed RGB format.                                                                                                                                                                                                                                                                                                                                                                                                       |
| ETC                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Standard OpenGL ES 2.0 texture compression format (for RGB)                                                                                                                                                                                                                                                                                                                                                                                                 |
| ETC2                                 | ?      | ?       | RGB      | ?                   | ?             | N/A                                                      | Ericsson Texture Compression - Compressed RGB format.                                                                                                                                                                                                                                                                                                                                                                                                       |
| ETC2                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Texture compression format that is supported in the OpenGL ES 3.0 API (for R, RG, RGB, and RGBA)                                                                                                                                                                                                                                                                                                                                                            |
| ETC                                  | ETC    | ?       | ?        | RGB                 | ?             | N/A                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC                                  | ETCA   | ?       | ?        | RGBA                | ?             | explicit                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ETC                                  | ETCI   | ?       | ?        | RGBA                | ?             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| EAC                                  | ?      | ?       | RG       | 11:11               | ?             | N/A                                                      | Two-channel (red and green) unsigned format. Each channel is decoded exactly as with EAC(R11) encoding.                                                                                                                                                                                                                                                                                                                                                     |
| EAC Signed                           | ?      | ?       | R        | 11                  | ?             | N/A                                                      | One-channel signed format. It allows preserving zero exactly, while still using both positive and negative values.                                                                                                                                                                                                                                                                                                                                          |
| EAC Signed                           | ?      | ?       | RG       | 11:11               | ?             | N/A                                                      | Two-channel (red and green) signed format. Each channel is decoded exactly as for EAC(SIGNED_R11).                                                                                                                                                                                                                                                                                                                                                          |
| EAC                                  | ?      | ?       | R        | 11 UNORM            | ?             | N/A                                                      | Unsigned R11 EAC                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| EAC                                  | ?      | ?       | R        | 11 SNORM            | ?             | N/A                                                      | Signed R11 EAC                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| EAC                                  | ?      | ?       | RG       | 11:11 UNORM         | ?             | N/A                                                      | Unsigned RG11 EAC                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| EAC                                  | ?      | ?       | RG       | 11:11 SNORM         | ?             | N/A                                                      | Signed RG11 EAC                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| EAC                                  | ?      | ?       | R        | 11                  | ?             | N/A                                                      | A single 16-bit component. Stored in the lower 16-bits (R and G) with little endian byte order of a 32-bit pixel of a PNG image with alpha.                                                                                                                                                                                                                                                                                                                 |
| EAC                                  | ?      | ?       | RG       | 11:11               | ?             | N/A                                                      | Two 16-bit components. Stored as two 16-bit values, in the lower (R and G) and upper (B and alpha) 16-bits of a PNG image with alpha.                                                                                                                                                                                                                                                                                                                       |
| EAC                                  | ?      | ?       | R        | 11 SIGNED           | ?             | N/A                                                      | A single signed 16-bit component.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| EAC                                  | ?      | ?       | RG       | 11:11 SIGNED        | ?             | N/A                                                      | Two signed 16-bit components.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ASTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | (magic number 0x5CA1AB13 LE, 0x13ABA15C BE) [webkit - Determine internal format of given astc compressed image through its header? - Stack Overflow](https://stackoverflow.com/questions/22600678/determine-internal-format-of-given-astc-compressed-image-through-its-header)                                                                                                                                                                              |
| ASTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | via ARM's encoder.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ASTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Most recent compressed texture format supported by Metal. Developed by AMD and supported fairly widely on OpenGL ES 3.0-class hardware, this format incorporates a selectable block size (from 4×4 to 12×12) that determines the compression ratio of the image. This unprecedented flexibility makes ASTC a very attractive choice, but it requires an A8 processor at a minimum, making it unusable on devices such as the iPhone 5s.                     |
| ASTC                                 | ASTC   | ?       | ?        | ?                   | ?             | ?                                                        | Adaptive Scalable Texture Compression                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ATC                                  | ATC    | ?       | RGB      | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATC                                  | ATCA   | ?       | RGBA     | ?                   | ?             | explicit                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATC                                  | ATCI   | ?       | RGBA     | ?                   | ?             | interpolated                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATCIA                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATC/AXT                              | ?      | ?       | RGB      | ?                   | ?             | ?                                                        | Compresses RGB textures with no alpha channel.                                                                                                                                                                                                                                                                                                                                                                                                              |
| ATC                                  | ?      | ?       | RGBA     | ?                   | ?             | explicit                                                 | Compresses RGBA textures using explicit alpha encoding (useful when alpha transitions are sharp).                                                                                                                                                                                                                                                                                                                                                           |
| ATC                                  | ?      | ?       | RGBA     | ?                   | ?             | interpolated                                             | Compresses RGBA textures using interpolated alpha encoding (useful when alpha transitions are gradient).                                                                                                                                                                                                                                                                                                                                                    |
| ATC                                  | ?      | ?       | RGB      | ?                   | ?             | ?                                                        | Compressed RGB format                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ATC                                  | ?      | ?       | RGBA     | ?                   | ?             | explicit                                                 | ARGB format with explicit alpha                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATC                                  | ?      | ?       | RGBA     | ?                   | ?             | interpolated                                             | ARGB format with interpolated alpha                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ATC                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Proprietary Adreno texture compression format (for RGB and RGBA)                                                                                                                                                                                                                                                                                                                                                                                            |
| ATC                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | similar to DXT (can convert from the last one)                                                                                                                                                                                                                                                                                                                                                                                                              |
| ATI1N                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Single component compression format using the same technique as DXT5 alpha. Four bits per pixel                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Two component compression format using the same technique as DXT5 alpha. Designed for compression object space normal maps. Eight bits per pixel                                                                                                                                                                                                                                                                                                            |
| ATI2N_XY                             | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Two component compression format using the same technique as DXT5 alpha. The same as ATI2N but with the channels swizzled. Eight bits per pixel                                                                                                                                                                                                                                                                                                             |
| ATI2N_DXT5                           | ?      | ?       | ?        | ?                   | ?             | ?                                                        | An ATI2N like format using DXT5. Intended for use on GPUs that do not natively support ATI2N. Eight bits per pixel                                                                                                                                                                                                                                                                                                                                          |
| 3Dc+                                 | ATI1   | BC4     | ?        | ?                   | ?             | ?                                                        | algorithm originally developed by ATI                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 3Dc/DXN                              | ATI2   | BC5     | ?        | ?                   | ?             | ?                                                        | algorithm originally developed by ATI. Implemented by Nvidia and ATI. It builds upon the earlier DXT5 algorithm and is an open standard                                                                                                                                                                                                                                                                                                                     |
| 3Dc                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | format is version of RGTC/BC5                                                                                                                                                                                                                                                                                                                                                                                                                               |
| LATC/3Dc+/ATI1                       | ?      | BC4     | R        | ?                   | 4             | ?                                                        | Grayscale, Useful for height maps, gloss maps, font atlases or any other grey-scale image                                                                                                                                                                                                                                                                                                                                                                   |
| ATI1/BC4U/AT1N/RGTC1_RED             | ATI1   | BC4U    | ?        | ?                   | 1:8           | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI1/BC4U/AT1N/RGTC1_RED             | BC4U   | BC4U    | ?        | ?                   | 1:8           | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| RGTC1S/BC4U/RGTC1U                   | BC4S   | BC4S    | ?        | ?                   | 1:8           | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2                                 | ?      | ATI2    | ?        | ?                   | 1:16          | ?                                                        | RGT2 variant with swapped R and G (3Dc)                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ATI1N                                | ?      | BC4     | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N                                | ?      | BC4     | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N/ATI2N_XY                       | ?      | BC5     | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N_DXT5                           | ?      | BC5     | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| RGTC2/SBC5S                          | BC5S   | BC5S    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| RGTC                                 | ?      | BC4     | ?        | UNORM               | 1:16          | ?                                                        | unsigned                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| RGTC                                 | ?      | BC4     | ?        | SNORM               | ?             | ?                                                        | signed                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| RGTC                                 | ?      | BC5     | ?        | UNORM               | ?             | ?                                                        | unsigned                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| RGTC                                 | ?      | BC5     | ?        | SNORM               | ?             | ?                                                        | signed                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| RGTC1/RGTC2 (BC4/BC5)                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | for one and two component textures.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| RGTC1                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Single-channel (red) compression format. Equivalent to BC4.                                                                                                                                                                                                                                                                                                                                                                                                 |
| RGTC2                                | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Two channel (red/green) compression format. Equivalent to BC5.                                                                                                                                                                                                                                                                                                                                                                                              |
| RGTC1                                | ?      | ?       | ?        | SIGNED              | ?             | ?                                                        | Signed version of RGTC1.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| RGTC2                                | ?      | ?       | ?        | SIGNED              | ?             | ?                                                        | Signed version of RGTC2.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ?                                    | BC4    | BC4     | R        | 8                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC5    | RG      | 8:8      | ?                   | ?             |                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC4S   | BC4S    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC4U   | BC4U    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC4    | ?       | ?        | ?                   | ?             | Single component compressed texture format for Microsoft |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC5    | BC5     | ?        | ?                   | ?             | ?                                                        | Two component compressed texture format for Microsoft                                                                                                                                                                                                                                                                                                                                                                                                       |
| ?                                    | BC6H   | BC6H    | ?        | ?                   | ?             | ?                                                        | High-Dynamic Range  compression format                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ?                                    | BC7    | ?       | ?        | ?                   | ?             | High-quality compression of RGB and RGBA data            |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ?                                    | BC6    | BC6     | RGB      | 8:8:8 half float    | ?             | ?                                                        | can natively store HDR images and is an excellent replacement for RGBM. DX11+                                                                                                                                                                                                                                                                                                                                                                               |
| ?                                    | BC7x   | BC7     | RGB      | 8:8:8               | ?             | ?                                                        | DX11+                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ?                                    | BC7x   | BC7     | RGBA     | 8:8:8               | ?             | ?                                                        | DX11+                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| RGTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | https://www.opengl.org/wiki/Red_Green_Texture_Compression                                                                                                                                                                                                                                                                                                                                                                                                   |
| RGTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | trivial adaptations of S3TC                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| RGTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | https://www.opengl.org/registry/specs/EXT/texture_compression_rgtc.txt                                                                                                                                                                                                                                                                                                                                                                                      |
| RGTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Mandatory in OpenGL 3.0 and OpenGL ES 3.0                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `RGTC1_SIGNED_RED`                   | ?      | BC4S    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| RGTC/3Dc                             | ?      | BC5     | RG       | ?                   | 8             | ?                                                        | Useful for tangent space normal maps. A two Channel Tangent Map                                                                                                                                                                                                                                                                                                                                                                                             |
| `RGTC2_SIGNED_RG`                    | ?      | BC5S    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI1N                                | ATI1   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N                                | ATI2   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N_XY                             | A2XY   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2N_DXT5                           | A2D5   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ATI2/AT2N/`RGTC2_RG`/ATIN/`ATIN2_XY` | ?      | BC5U    | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| BPTC                                 | ?      | BC6H    | ?        | UFLOAT_BLOCK        | ?             | ?                                                        | unsigned version                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| BPTC                                 | ?      | BC6H    | ?        | SFLOAT_BLOCK        | ?             | ?                                                        | signed version                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| BPTC                                 | ?      | BC7     | ?        | UNORM_BLOCK         | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| BPTC                                 | ?      | BC7     | ?        | SRGB_BLOCK          | ?             | ?                                                        | sRGB-encoded                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| BPTC                                 | ?      | BC7     | ?        | ?                   | ?             | ?                                                        | a high-quality RGBA compression format.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| BPTC                                 | ?      | BC6H    | ?        | UF16 FLOAT          | ?             | ?                                                        | for linear and HDR textures                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| BPTC                                 | ?      | BC6H    | ?        | SF16 SIGNED_FLOAT   | ?             | ?                                                        | for linear and HDR textures                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| BPTC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | High quality recent 128-bit compressed format, also known as BC7. Supports alpha.                                                                                                                                                                                                                                                                                                                                                                           |
| BPTC                                 | ?      | ?       | ?        | FLOAT               | ?             | ?                                                        | Half-float RGB format, also known as BC6H_UF16. --hdr option supported for HDR textures.                                                                                                                                                                                                                                                                                                                                                                    |
| BPTC                                 | ?      | ?       | ?        | SIGNED_FLOAT        | ?             | ?                                                        | Signed half-float format, also known as BC6H_SF16.                                                                                                                                                                                                                                                                                                                                                                                                          |
| BPTC                                 | ?      | BC6H    | ?        | ?                   | ?             | ?                                                        | algorithm originally developed by NVIDIA                                                                                                                                                                                                                                                                                                                                                                                                                    |
| BPTC                                 | ?      | BC7     | ?        | ?                   | ?             | ?                                                        | algorithm originally developed by NVIDIA                                                                                                                                                                                                                                                                                                                                                                                                                    |
| BPTC                                 | ?      | BC6H    | RGB      | ?                   | 8             | ?                                                        | Fast Compression, Useful for HDR 16 images only on DX11+ level hardware                                                                                                                                                                                                                                                                                                                                                                                     |
| BPTC                                 | ?      | BC6H    | RGB      | ?                   | 8             | ?                                                        | Fine Compression, Same as above with longer optimized compression time for a finer result                                                                                                                                                                                                                                                                                                                                                                   |
| BPTC                                 | ?      | BC7     | RGBA     | ?                   | 8             | ?                                                        | Fast Compression, Useful for high quality color maps, color maps with full alpha.  It provides the best quality compression only on DX11+ level hardware                                                                                                                                                                                                                                                                                                    |
| BPTC                                 | ?      | BC7     | RGBA     | ?                   | 8             | ?                                                        | Fine Compression, Same as above with longer optimized compression time for a finer result                                                                                                                                                                                                                                                                                                                                                                   |
| BPTC                                 | ?      | BC7     | RGBA     | sRGBA               | 8             | ?                                                        | Fast Compression, Same as BC7 Fast above with sRGB extended header only on DX10 + level hardware                                                                                                                                                                                                                                                                                                                                                            |
| BPTC                                 | ?      | BC7     | RGBA     | sRGBA               | 8             | ?                                                        | Fine Compression, Same as BC7 Fine above with sRGB extended header only on DX10 + level hardware                                                                                                                                                                                                                                                                                                                                                            |
| LATC                                 | ?      | ?       | ?        | ?                   | ?             | ?                                                        | trivial adaptations of S3TC                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| VTC                                  | ?      | ?       | ?        | ?                   | ?             | ?                                                        | Volume Texture Compression (VTC) is analogous to the S3TC texture compression formats                                                                                                                                                                                                                                                                                                                                                                       |
| GT                                   | GT1x   | ?       | ?        | ?                   | ?             | ?                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

| Name | FourCC | DX name | Channels | Depth (bit/channel) | rate (bit/px) | Alpha | Comment                                   |
|------|--------|---------|----------|---------------------|---------------|-------|-------------------------------------------|
| ASTC | ?      | ?       | L        | ?                   | ?             | ?     | Luminance-only                            |
| ASTC | ?      | ?       | LA       | ?                   | ?             | ?     | Luminance with transparency               |
| ASTC | ?      | ?       | L+A      | ?                   | ?             | ?     | Luminance with uncorrelated transparency  |
| ASTC | ?      | ?       | X+Y      | ?                   | ?             | ?     | Surface normals                           |
| ASTC | ?      | ?       | RGB      | ?                   | ?             | ?     | Full color                                |
| ASTC | ?      | ?       | XY+Z     | ?                   | ?             | ?     | Surface normals with uncorrelated Z       |
| ASTC | ?      | ?       | RGBA     | ?                   | ?             | ?     | Full color with transparency              |
| ASTC | ?      | ?       | RGB+A    | ?                   | ?             | ?     | Full color with uncorrelated transparency |

| Name         | FourCC | DX name | Channels | Depth (bit/channel) | rate (bit/px) | Alpha | Comment                                                                                      |
|--------------|--------|---------|----------|---------------------|---------------|-------|----------------------------------------------------------------------------------------------|
| Uncompressed | ?      | ?       | RGBA     | 8:8:8:8             | 32            | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | ARGB     | 8:8:8:8             | 32            | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RGB      | 8:8:8               | 24            | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RG       | 8                   | 8             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | R        | 8                   | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | ARGB     | 2:10:10:10          | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | ARGB     | 16:16:16:16         | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RG       | 16:16               | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | R        | 16:16               | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | ARGB     | 16:16:16:16 FLOAT   | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RG       | 16:16 FLOAT         | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | R        | 16 FLOAT            | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | ARGB     | 32:32:32:32 FLOAT   | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RG       | 32:32 FLOAT         | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | R        | 32 FLOAT            | ?             | ?     | Uncompressed                                                                                 |
| Uncompressed | ?      | ?       | RGB      | HALF_FLOAT          | ?             | ?     | Uncompressed format where each color component is stored in a 16-bits floating point number. |
| Uncompressed | ?      | ?       | RGBA     | HALF_FLOAT          | ?             | ?     | Includes alpha.                                                                              |
| P1           | P1     | ?       | ?        | ?                   | ?             | ?     | 1-bit palletized                                                                             |
| P2           | P2     | ?       | ?        | ?                   | ?             | ?     | 2-bit palletized                                                                             |
| P4           | P4     | ?       | ?        | ?                   | ?             | ?     | 4-bit palletized                                                                             |
| P8           | P8     | ?       | ?        | ?                   | ?             | ?     | ATI Palette8 8-bit palletized                                                                |
| G1           | G1     | ?       | ?        | ?                   | ?             | ?     | 1-bit gray-scale                                                                             |
| G2           | G2     | ?       | ?        | ?                   | ?             | ?     | 2-bit gray-scale                                                                             |
| G4           | G4     | ?       | ?        | ?                   | ?             | ?     | 4-bit gray-scale                                                                             |
| G8           | G8     | ?       | ?        | ?                   | ?             | ?     | 8-bit gray-scale                                                                             |
| G16          | G16    | ?       | ?        | ?                   | ?             | ?     | 16-bit gray-scale                                                                            |
| AG1          | AG1    | ?       | ?        | ?                   | ?             | ?     | 1-bit gray-scale with alpha                                                                  |
| AG2          | AG2    | ?       | ?        | ?                   | ?             | ?     | 2-bit gray-scale with alpha                                                                  |
| AG4          | AG4    | ?       | ?        | ?                   | ?             | ?     | 4-bit gray-scale with alpha                                                                  |
| AG8          | AG8    | ?       | ?        | ?                   | ?             | ?     | 8-bit gray-scale with alpha                                                                  |
| A1           | A1     | ?       | ?        | ?                   | ?             | ?     | 1-bit alpha                                                                                  |
| A2           | A2     | ?       | ?        | ?                   | ?             | ?     | 2-bit alpha                                                                                  |
| A4           | A4     | ?       | ?        | ?                   | ?             | ?     | 4-bit alpha                                                                                  |
| A8           | A8     | ?       | ?        | ?                   | ?             | ?     | 8-bit alpha                                                                                  |
| APC1         | APC1   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| APC2         | APC2   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| APC3         | APC3   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| APC4         | APC4   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| APC5         | APC5   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| APC6         | APC6   | ?       | ?        | ?                   | ?             | ?     |                                                                                              |
| UYVY         | UYVY   | ?       | UYVY     | 4:2:2               | ?             | ?     |                                                                                              |
| YUY2         | YUY2   | ?       | YUYV     | 4:2:2               | ?             | ?     |                                                                                              |

### Basis Universal

> Basis Universal is a ["supercompressed"](http://gamma.cs.unc.edu/GST/gst.pdf) GPU texture compression system that outputs a highly compressed intermediate file format (.basis) that can be quickly transcoded to a [very wide variety](https://github.com/BinomialLLC/basis_universal/wiki/OpenGL-texture-format-enums-table) of GPU compressed and uncompressed pixel formats: ASTC 4x4 L/LA/RGB/RGBA, PVRTC1 4bpp RGB/RGBA, PVRTC2 RGB/RGBA, BC7 mode 6 RGB, BC7 mode 5 RGB/RGBA, BC1-5 RGB/RGBA/X/XY, ETC1 RGB, ETC2 RGBA, ATC RGB/RGBA, ETC2 EAC R11 and RG11, FXT1 RGB, and uncompressed raster image formats 8888/565/4444.

- [BinomialLLC/basis_universal: Basis Universal GPU Texture Codec](https://github.com/BinomialLLC/basis_universal)
- [Supercompressed texture](#supercompressed-texture)

### KTX

KTX is the standard compression format, used as a container for multiple images/textures, and is ideal for mipmapping.
Khronos provides an open source C library (libktx) in which KTX texture loading with mipmaps is supported. \[...\] This function (ktxLoadTextureM) was provided in [the library (libktx)](https://www.khronos.org/opengles/sdk/tools/KTX/doc/libktx/)

```c
UINT8 * LoadKTX(const CHAR * strFileName , UINT32 *pWidth , UINT32 * pHeight , UINT32 * nFormat , UINT32 * nSize){
	typedef struct KTX_header_t {
		UINT8  identifier[12];
		UINT32  endianness;
		UINT32  glType;
		UINT32  glTypeSize;
		UINT32  glFormat;
		UINT32  glInternalFormat;
		UINT32  glBaseInternalFormat;
		UINT32  pixelWidth;
		UINT32  pixelHeight;
		UINT32  pixelDepth;
		UINT32  numberOfArrayElements;
		UINT32  numberOfFaces;
		UINT32  numberOfMipmapLevels;
		UINT32  bytesOfKeyValueData;
	} KTX_Header;

	typedef struct KTX_texinfo_t {
		UINT32  textureDemensions;
		UINT32  glTarget;
		UINT32 compressed;
		UINT32 generateMipmaps;
	} KTX_Texinfo;

	KTX_Header header;
	KTX_Texinfo texinfo;
	UINT8 * data = NULL;
	UINT32 dataSize = 0;
	UINT32 texname;
	int texnameUser;
	UINT32 faceLodSize;
	UINT32  faceLodSizeRounded;
	UINT32 level;
	UINT32 face;

	// Read the file
	FILE* file = fopen( strFileName, "rb" );

	if( NULL == file )
		return NULL;

	//read the header of ktx file
	fread( &header, sizeof(header), 1, file );

	//
	fseek(file,(long)header.bytesOfKeyValueData,SEEK_CUR);
	fread(&faceLodSize,sizeof(faceLodSize),1,file);

	faceLodSizeRounded = (faceLodSize + 3) & ~(UINT32)3;
	data = (UINT8 *)malloc(faceLodSizeRounded);

	fread(data,faceLodSizeRounded,1,file);

	*pWidth = header.pixelWidth;
	*pHeight= header.pixelHeight;
	*nSize = faceLodSizeRounded;
	*nFormat = header.glInternalFormat;

	return data;
}
```

### PKM

PKM is a simple file format used mainly to contain single compressed images. Generating mipmaps in this case would create multiple PKM files instead of a single file, and so as a consequence, this format is not recommended for that purpose.

### ATF

Adobe Texture Format

- https://github.com/away3d/away3d-core-openfl/blob/4916415870c8cb4e566363c95074c8f7c969c653/away3d/textures/ATFData.hx
- [ATF File Format](https://www.adobe.com/devnet/archive/flashruntimes/articles/atf-file-format.html)
- https://archive.is/http://www.adobe.com/devnet/flashruntimes/articles/introducing-compressed-textures.html
- [ATF SDK user's guide | Adobe Developer Connection](http://wayback.archive.org/web/20140526003120/http://www.adobe.com/devnet/flashruntimes/articles/atf-users-guide.html)

### ATC/ATITC/AXT

ATITC (ATI texture compression)

OpenGL extension `GL_ATI_texture_compression_atitc` is an alias of [`GL_AMD_compressed_ATC_texture`](https://www.khronos.org/registry/gles/extensions/AMD/AMD_compressed_ATC_texture.txt) (not all platform implement it)

ATC is AMD's proprietary compression algorithm for compressing textures for handheld devices to save on power consumption, memory footprint and bandwidth.

Implemented Qualcomm (and previously ATI then AMD). See https://en.wikipedia.org/wiki/Adreno#History

Called AXT because it is very similar to DXT codec:

- [2012.Converting.DXTC.to.ATC.pdf](http://www.guildsoftware.com/papers/2012.Converting.DXTC.to.ATC.pdf)
- https://twitter.com/p1xelcoder/status/394863589367902208

For the texture:

One 4x4 bloc, use ATC explicit (ATCA), with following pixels:

```
RGRG
GGRG
RRRG
GGGG
```

Where R = Red, G = Green
And the top-left pixel semi transparent (58% A=0x69)

To create it use:

```sh
printf '\xFF\x00\x00\x69\x00\xFF\x00\xFF\xFF\x00\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\xFF\x00\x00\xFF\x00\xFF\x00\xFF\xFF\x00\x00\xFF\xFF\x00\x00\xFF\xFF\x00\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF\x00\xFF' | convert -depth 8 -size 4x4+0 rgba:- image4x4.png
```

Compress it, then you get the following bloc data:

```
F6 FF FF FF FF FF FF FF 00 7C E0 07 CC CF C0 FF
```

The RGB color part:

```
00 7C E0 07 CC CF C0 FF
```

```
encodingMethod = 00 7C (LE), 0x7C00 = first bit (0x7C00 >> 15) = 0
color0 = 00 7C (LE), 0x7C00 = (skip first bit),0b11111,0b00000,0b00000 = 31,0,0 = rgb(255,0,0)
color1 = E0 07 (LE), 0x07E0 = 0b00000,0b111111,0b00000 = 0,63,0 = rgb(0,255,0)
p0_0 = 11 => color1
p1_0 = 00 => color0
p2_0 = 11 => color1
p3_0 = 00 => color0
p0_1 = 11 => color1
p1_1 = 00 => color0
p2_1 = 11 => color1
p3_1 = 11 => color1
p0_2 = 11 => color1
p1_2 = 00 => color0
p2_2 = 00 => color0
p3_2 = 00 => color0
p0_3 = 11 => color1
p1_3 = 11 => color1
p2_3 = 11 => color1
p3_3 = 11 => color1
```

- https://www.khronos.org/registry/gles/extensions/AMD/AMD_compressed_ATC_texture.txt
- [\[REF\][11.11.09] CFC - THE Manila/TF3D Image … | Windows Mobile Development and Hacking](http://forum.xda-developers.com/showthread.php?t=437777#postcount2798443)

#### QTC

Qualcomm adapted version of ATC used by Manila/Mode9

> Find an x, with which a following expression has a minimum value (of F):
>
> ````
> F(x) = 30 * (r - R)^2 + 59 * (g - G)^2 + 11 * (b - B)^2
> where
> r = x * r1 + (1 - x) * r2
> g = x * g1 + (1 - x) * g2
> r = x * g1 + (1 - x) * g2
> ````
>
> Basically, we need to find a function MinX(R, G, B, r1, g1, b1, r2, g2, b2) which value will turn F(x) into minimum value, and 0 <= MinX <= 1
>
> I guess in the last equation all r and g should be replaced by b.
> In that case, according to Maple, the solution of dF(x)/dx = 0 is:
> ````
> x = (-30*r2*r1+30*r2^2+30*R*r1-30*R*r2-59*g2*g1+
> 59*g2^2+59*G*g1-59*G*g2-11*b2*b1+11*b2^2+
> 11*B*b1-11*B*b2)/
> (30*r1^2-60*r2*r1+30*r2^2+59*g1^2-118*g2*g1+
> 59*g2^2+11*b1^2-22*b2*b1+11*b2^2)
> ````

> 0x0000: xx xx xx xx xx xx xx xx - transparency data. 1-byte/pixel. But you may ask: hey! there're 16 pixels per chunk! Wtf? Sorry guys, QTC image is actually halved by width and restored via interpolation during decoding.
> Bytes are drawn in this order:
>
> ````
> [i2][0][i][1]
> [i2][2][i][3]
> [i2][4][i][5]
> [i2][6][i][7]
> ````
>
> "i" means interpolated pixel, "i2" means pixel, interpolated between 2 chunks
> also, FYI, tflo3d wrap's image around during edge interpolation
>
> ````
> 0x0008: xx xx - color non-uniformity info. see next. also, dunno how it works yet
>
> 0x000a: BB RG - key chunk color in RGB format (8 bits for blue, and 4+4 bits for red+green). Yes, pixels in chunk have shared color, modified by previous 2 and next 4 bytes
>
> 0x000c: 21 43 65 87 - ligthness values for each drawn pixel (number corresponds to pixel #), 4bits each
> ````

> . QTC files
> They're non-compressed bitmaps, but encoding used there is completely retarded.
> As ryujakk *almost* correctly stated, header is:
>
> ````
> 0x0000: 51 54 43 31 01(?) - magic bytes signature
> 0x0008: xx xx xx xx - UINT32 image width
> 0x000c: xx xx xx xx - UINT32 image height
> 0x0010: .... some metadata goes here, maybe encoding type too, dunno yet
> 0x0020: image data
> 0x......: last ~500 bytes are padded with zeros for some reason (> QTC files are padded up to multiples of 512. For faster loading, i reckon.)
>
> 0x0008: xx xx - Key color 1. Color is calculated by adding values from 4 LUTs (lookup tables) for each 4 bits. Each LUT holds RGB values
>
> 0x000a: xx xx - Key color 2. Same as key color 1, but different LUTs
>
> 0x000c: 21 43 65 87 - mixdown coefficients for each drawn pixel (number corresponds to pixel #), 4bits each. see next
> ````
>
> As i wrote earlier, pixels in chunk have shared master colors. The resulting is calulated as:
>
> ````
> color = mixdown * key_color_2 + (1 - mixdown) * key_color_1
> ````
>
> Note 1. Mixdown value is normalized to 1
> Note 2. Mixdown operation s/b done for each color channel distinctly

### ASTC

KTX can contains ASTC data1

Adopted by official extension for both OpenGL 3.0

1:1 S3TC/DXT1->ASTC bitwise mapping possible

```js
// See https://wolfwings.us/webgl/ WebGL Book Viewer

// Conversion from S3TC->ASTC weighting:
// 0 -> 0 ->  0/63 ->  0/64
// 1 -> 7 -> 63/63 -> 64/64
// 2 -> 5 -> 45/63 -> 46/64
// 3 -> 2 -> 18/63 -> 18/64
//
// This is due to ASTC specifying that
// weighting is always expanded to six
// bits, then greater than 31 gets one
// added, so it becomes 0-64/64 scale.
//
// Also ASTC specifies bits in reverse
// order of S3TC for the weight map so
// this is reversing the S3TC value as
// part of the table lookup for free.

// w5w5w6w6w6w7w7w7
const astc_weight_map_0 = [
0b11111111,0b00111111,0b01111111,0b10111111,0b11000111,0b00000111,0b01000111,0b10000111,
0b11101111,0b00101111,0b01101111,0b10101111,0b11010111,0b00010111,0b01010111,0b10010111,
0b11111000,0b00111000,0b01111000,0b10111000,0b11000000,0b00000000,0b01000000,0b10000000,
0b11101000,0b00101000,0b01101000,0b10101000,0b11010000,0b00010000,0b01010000,0b10010000,
0b11111101,0b00111101,0b01111101,0b10111101,0b11000101,0b00000101,0b01000101,0b10000101,
0b11101101,0b00101101,0b01101101,0b10101101,0b11010101,0b00010101,0b01010101,0b10010101,
0b11111010,0b00111010,0b01111010,0b10111010,0b11000010,0b00000010,0b01000010,0b10000010,
0b11101010,0b00101010,0b01101010,0b10101010,0b11010010,0b00010010,0b01010010,0b10010010];

// ........w4w4w4w5
const astc_weight_map_1 = [
0b00001111,0b00000001,0b00001011,0b00000101,0b00001110,0b00000000,0b00001010,0b00000100];

// w2w3w3w3........
const astc_weight_map_2 = [
0b11110000,0b01110000,0b11110000,0b01110000,0b10000000,0b00000000,0b10000000,0b00000000,
0b11010000,0b01010000,0b11010000,0b01010000,0b10100000,0b00100000,0b10100000,0b00100000];

// w0w0w0w1w1w1w2w2
const astc_weight_map_3 = [
0b11111111,0b00011111,0b10111111,0b01011111,0b11100011,0b00000011,0b10100011,0b01000011,
0b11110111,0b00010111,0b10110111,0b01010111,0b11101011,0b00001011,0b10101011,0b01001011,
0b11111100,0b00011100,0b10111100,0b01011100,0b11100000,0b00000000,0b10100000,0b01000000,
0b11110100,0b00010100,0b10110100,0b01010100,0b11101000,0b00001000,0b10101000,0b01001000,
0b11111110,0b00011110,0b10111110,0b01011110,0b11100010,0b00000010,0b10100010,0b01000010,
0b11110110,0b00010110,0b10110110,0b01010110,0b11101010,0b00001010,0b10101010,0b01001010,
0b11111101,0b00011101,0b10111101,0b01011101,0b11100001,0b00000001,0b10100001,0b01000001,
0b11110101,0b00010101,0b10110101,0b01010101,0b11101001,0b00001001,0b10101001,0b01001001];

// Standard 5-bit to 8-bit color expansion
const astc_color_map_5 = Array.from( Array( 32 ).keys() ).map( ( v, i ) => Math.floor( i * 8.25 ) ); // * 33 / 4

// Standard 6-bit to 8-bit color expansion
const astc_color_map_6 = Array.from( Array( 64 ).keys() ).map( ( v, i ) => Math.floor( i * 4.0625 ) ); // * 65 / 16

function convert_astc( data ) {
	var buffer = new ArrayBuffer( data.byteLength * 2 );
	var large = new Uint8Array( buffer );
	var small = new Uint8Array( data );
	for ( var p = 0; p < data.byteLength; p += 8 ) {
		var c0 = ( small[p + 1] << 8 ) + small[p   ];
		var b0 = astc_color_map_5[   c0         & 31 ];
		var g0 = astc_color_map_6[ ( c0 >>  5 ) & 63 ];
		var r0 = astc_color_map_5[   c0 >> 11        ];

		var c1 = ( small[p + 3] << 8 ) + small[p + 2];
		var b1 = astc_color_map_5[   c1         & 31 ];
		var g1 = astc_color_map_6[ ( c1 >>  5 ) & 63 ];
		var r1 = astc_color_map_5[   c1 >> 11        ];

		if ( ( r0 + g0 + b0 ) < ( r1 + g1 + b1 ) ) {
			[r0, r1] = [r1, r0];
			[g0, g1] = [g1, g0];
			[b0, b1] = [b1, b0];
			small[p + 4] ^= 0x55;
			small[p + 5] ^= 0x55;
			small[p + 6] ^= 0x55;
			small[p + 7] ^= 0x55;
		}

		large[p + p     ] = 0x53;
		large[p + p +  1] = 0x00;
		large[p + p +  2] =           1 | ( r1 << 1 );
		large[p + p +  3] = ( r1 >> 7 ) | ( r0 << 1 );
		large[p + p +  4] = ( r0 >> 7 ) | ( g1 << 1 );
		large[p + p +  5] = ( g1 >> 7 ) | ( g0 << 1 );
		large[p + p +  6] = ( g0 >> 7 ) | ( b1 << 1 );
		large[p + p +  7] = ( b1 >> 7 ) | ( b0 << 1 );
		large[p + p +  8] = ( b0 >> 7 );
		large[p + p +  9] = 0;
		large[p + p + 10] = astc_weight_map_0[small[p + 7] >> 2];
		large[p + p + 11] = astc_weight_map_1[small[p + 7] &  7] | astc_weight_map_2[small[p + 6] >> 4];
		large[p + p + 12] =                                        astc_weight_map_3[small[p + 6] & 63];
		large[p + p + 13] = astc_weight_map_0[small[p + 5] >> 2];
		large[p + p + 14] = astc_weight_map_1[small[p + 5] &  7] | astc_weight_map_2[small[p + 4] >> 4];
		large[p + p + 15] =                                        astc_weight_map_3[small[p + 4] & 63];
	}
	return buffer;
}

// For S3TC with an image with exact dimensions,
// byteLength = (width / 4) * (height / 4) * 8
// byteLength = width * 0.25 * height * 0.25 * 8
// byteLength = width * height * 0.5
// byteLength / 0.5 = width * height
// byteLength * 2 = width * height
// (byteLength * 2) / height = width
// ...with a fixed height of 1080...
// (byteLength * 2) / 1080 = width
// byteLength / 540 = width
```


Adaptive Scalable Texture Compression (ASTC)

| Encoding Format | Description                               |
|-----------------|-------------------------------------------|
| L               | Luminance-only                            |
| LA              | Luminance with transparency               |
| L+A             | Luminance with uncorrelated transparency  |
| X+Y             | Surface normals                           |
| RGB             | Full color                                |
| XY+Z            | Surface normals with uncorrelated Z       |
| RGBA            | Full color with transparency              |
| RGB+A           | Full color with uncorrelated transparency |

Three compression formats are introduced:

- A compression format for RGB textures.
- A compression format for RGBA textures using explicit alpha encoding.
- A compression format for RGBA textures using interpolated alpha encoding.

- ATCA/ATC explicit
- ATCI/ATC interpolated
- ASTC LDR
- ASTC HDR

ASTC LDR is a new texture compression format. The level of image degradation is in general remarkably low given the compression ratio achieved. The user is able to control the quality/size trade-off by selecting one of a number of different block sizes.
Note: The format supports NPOT textures. It can hold data for up to four 8-bit components per texel and supports both linear RGB and sRGB color spaces.
If working with floating point data, ASTC LDR is not suitable — consider using ASTC HDR instead.

	/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/texturetool -e ASTC --compression-mode-exhaustive --bits-per-pixel-4 -f KTX -o image.ktx image.png

- ASTC Encoder by ARM and AMD https://github.com/ARM-software/astc-encoder
- [Adaptive Scalable Texture Compression — Wikipedia](https://en.wikipedia.org/wiki/Adaptive_Scalable_Texture_Compression)
- [ASTC Texture Compression - OpenGL.org](https://www.opengl.org/wiki/ASTC_Texture_Compression)
- [ASTC Texture Compression - Mali Developer Center](http://malideveloper.arm.com/resources/sample-code/astc-textures/)
- [ASTC-GDC2013.pdf](http://malideveloper.arm.com/downloads/ASTC-GDC2013.pdf)

#### ASTC Container

`.atc`

The ASTC container format is custom-tailored to the ASTC compression format. The header indicates the compression block size, which allows you to select the correct pixel format when loading the data into texture memory and calculate the length of the texture data. Here is the layout of the ASTC header:

```c
struct ASTCHeader {
	uint32_t magic;
	unsigned char blockDimX;
	unsigned char blockDimY;
	unsigned char blockDimZ;
	unsigned char xSize[3];
	unsigned char ySize[3];
	unsigned char zSize[3];
};
```

The `xSize`, `ySize`, and `zSize` fields are 24-bit quantities, each encoded as three bytes. The compressed image data immediately follows the header.

### Other formats

- [Floating-point formats](https://www.khronos.org/registry/dataformat/specs/1.1/dataformat.1.1.html#fpformats)

```c
// from https://github.com/libgdx/libgdx/blob/155fd6972e7084862ccdba9b12894538685416ff/gdx/jni/gdx2d/gdx2d.c#L52-L83
static inline uint32_t to_format(uint32_t format, uint32_t color) {
	uint32_t r, g, b, a, l;

	switch(format) {
		case GDX2D_FORMAT_ALPHA:
			return color & 0xff;
		case GDX2D_FORMAT_LUMINANCE_ALPHA:
			r = (color & 0xff000000) >> 24;
			g = (color & 0xff0000) >> 16;
			b = (color & 0xff00) >> 8;
			a = (color & 0xff);
			l = ((uint32_t)(0.2126f * r + 0.7152 * g + 0.0722 * b) & 0xff) << 8;
			return (l & 0xffffff00) | a;
		case GDX2D_FORMAT_RGB888:
			return color >> 8;
		case GDX2D_FORMAT_RGBA8888:
			return color;
		case GDX2D_FORMAT_RGB565:
			r = (((color & 0xff000000) >> 27) << 11) & 0xf800;
			g = (((color & 0xff0000) >> 18) << 5) & 0x7e0;
			b = ((color & 0xff00) >> 11) & 0x1f;
			return r | g | b;
		case GDX2D_FORMAT_RGBA4444:
			r = (((color & 0xff000000) >> 28) << 12) & 0xf000;
			g = (((color & 0xff0000) >> 20) << 8) & 0xf00;
			b = (((color & 0xff00) >> 12) << 4) & 0xf0;
			a = ((color & 0xff) >> 4) & 0xf;
			return r | g | b | a;
		default:
			return 0;
	}
}
```

Note: RGBA4444 = 16bit **but not related to paletted**

- [How to create a texture optimized for conversion to RGBA-4444 - YouTube](https://www.youtube.com/watch?v=v1xGYecsnX0)
	See `4bitGrayscale.gpl`

	Use a palette mode, with gray scale colors:

	```
	0 0 0
	17 17 17
	34 34 34
	51 51 51
	68 68 68
	85 85 85
	102 102 102
	119 119 119
	136 136 136
	153 153 153
	170 170 170
	187 187 187
	204 204 204
	221 221 221
	238 238 238
	255 255 255
	```

`PALETTE8_RGBA8_OES` can be used with `compressedTexImage2D()` to upload paletted colors (like from PNG8): https://www.opengl.org/registry/specs/OES/OES_compressed_paletted_texture.txt

## Supercompressed texture

![Textures types](http://gamma.cs.unc.edu/GST/images/teaser.png)

## Hardware

**TODO make a table with colons:**

1. Model
2. Release date
3. Status (Discontinued, Current)
4. GPU Maker
5. GPU Kind
6. GPU Model
7. GPU Clock
8. APIs support (DirectX, OpenGL, OpenCL, etc.)
9. 3dmarks rate (PassMark, 3DMark)
	- [GPU performance comparison](http://alteredqualia.com/tools/gpus/)
	- [Smartphone Graphics Cards - Benchmark List - NotebookCheck.net Tech](https://www.notebookcheck.net/Smartphone-Graphics-Cards-Benchmark-List.149363.0.html)
	- [Mobile Graphics Cards - Benchmark List - NotebookCheck.net Tech](https://www.notebookcheck.net/Mobile-Graphics-Cards-Benchmark-List.844.0.html)
	- [PassMark Android Benchmark 3D Graphics Rating Charts](http://www.androidbenchmark.net/g3dmark_chart.html)
	- [PassMark iOS, iPhone, iPod Touch, iPad Benchmark 3D Graphics Rating Charts](http://www.iphonebenchmark.net/g3dmark_chart.html)
	- [Best Smartphones and Tablets April - 2017](https://www.futuremark.com/hardware/mobile)

We can't know quantity produce and market share by year

https://www.scientiamobile.com/page/movr-mobile-overview-report
- [CPU-Z | Softwares | CPUID](http://www.cpuid.com/softwares/cpu-z.html)
- `adb shell dumpsys | grep GLES` -> `GLES: Qualcomm, Adreno (TM) 330, OpenGL ES 3.0 V@53.0 AU@ (CL@)`
- (Java Android) `String renderer = GLES20.glGetString(GLES20.GL_RENDERER);` `GL10.GL_VENDOR` `GL10.GL_VERSION` `GL10.GL_EXTENSIONS`

> All Apple devices with A8 or later CPUs, and more than 90%
> of Android devices support ASTC on mobile, with S3TC being
> supported on 100% of PC platforms since the late 90's.

Get list and market share:

- https://en.wikipedia.org/wiki/Comparison_of_tablet_computers
- https://en.wikipedia.org/wiki/Smartphone
- https://en.wikipedia.org/wiki/Tablet_computer
- [PassMark - Android phone model listing](http://www.androidbenchmark.net/device_list.php)
- [PassMark Android Benchmark Charts - Popular Phones](http://www.androidbenchmark.net/popular_chart.html)

- S3TC/DXT
	- All desktop (Nvidia, ATI/AMD, Intel)
	- some mobile devices
	- NVIDIA Tegra 2 chipset integrated into Motorola products such as XOOM and ATRIX
- PVRTC
	- All PowerVR GPUs
	- iPhone or iPad
	- Nexus S, Kindle fire
	- HTC EVO (PowerVR SGX 531 version)
	- some Motorola devices, such as those in the DROID by Motorola series
	- BlackBerry Z10 STL100-1 (PowerVR)
- PVRTC2
	- All PowerVR Series5XT, Series6
	- Apple A8+ devices using OpenGL ES 3.0
- ASTC
	- Qualcomm Adreno 420
	- Adreno 4xx adds support for ASTC LDR compression, which is made available through the Android Extension Pack
	- Intel HD Graphics Gen9+
	- Nexus One
	- BlackBerry Z10 STL100-2, Z10 STL100-3, Z10 STL100-4, Q10 SQN, DAC SQN, Q5 SQR (Qualcomm)
	- Nvidia's Kepler and Maxwell-based Tegra
	- ARM Mali-T620, Mali-T720, Mali-T760, Mali-T820/T830, Mali-T860/T880 and Mali-G71 [Mali (GPU) — Wikipedia](https://en.wikipedia.org/wiki/Mali_%28GPU%29)
- ATITC/ATC
	- Adreno GPU: all Qualcomm Snapdragon devices
	- HTC EVO (Adreno 200 version)
	- HTC G1 and HTC Hero
	- LG Nexus 5X (Adreno 418)
	- Sony Ericsson Android™ phones such as the Xperia™ X10 or Xperia™ PLAY (Qualcomm Adreno 200 and 205)
- ETC1
	- most of Android devices
	- Intel HD Graphics Gen8+
	- Qualcomm Adreno 3xx
- ETC2
	- all compatible GPU with OpenGL 3.0
	- Qualcomm Adreno 3xx
- RGTC
	- all compatible GPU with OpenGL 3.0
	- Nvidia GeForce 8 Series https://www.opengl.org/registry/specs/EXT/texture_compression_rgtc.txt

Adreno 530 compatible Vulkan

GPU Vendor (09/2016):

- ARM (ETC): 35.9%
- Qualcomm (ATC): 32.4%
- Apple (PVRTC): 16.0%
- ImgTec (PVRTC): 11.2%
- Vivante (DXT): 1.9%
- Broadcom (ETC): 1.1%
- NVIDIA (DXT): 0.7%

GPU Model (09/2016):

- Adreno (ASTC): 32.3%
- Mali <450: 21.2%
- ImgTec (PVRTC): 27.2%
- Mali T600+ (ASTC): 14.6%
- Vivante (DXT): 1.8%
- Videocore IV (?): 1.1%
- Intel: 0.3%
- Nvidia (DXT): 0.3%
- Emulators: 0.7%
	- Android ES Emulator (GeForce): 0.4%
	- BlueStacks ES2.0 Emu: 0.3%

- Imagination Technologies PowerVR http://withimagination.imgtec.com/wp-content/uploads/2013/03/Why_use_PVRTC.png https://en.wikipedia.org/wiki/PowerVR and https://imgtec.com/powervr/graphics/
- ARM Mali https://www.arm.com/products/graphics-and-multimedia/mali-gpu and https://developer.arm.com/products/graphics-and-multimedia/mali-gpus
- Nvidia GPUs https://en.wikipedia.org/wiki/List_of_Nvidia_graphics_processing_units
- https://www.techpowerup.com/gpudb/
- Qualcomm Adreno https://en.wikipedia.org/wiki/Adreno https://www.qualcomm.com/products/snapdragon/gpu-specifications and https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu
- Broadcom VideoCore https://en.wikipedia.org/wiki/VideoCore#3D_engine
- Intel GPUs (some are PowerVR based) https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units_(2013_or_earlier) https://en.wikipedia.org/wiki/Intel_HD_and_Iris_Graphics https://fr.wikipedia.org/wiki/Intel_HD_Graphics http://www.intel.com/content/www/us/en/architecture-and-technology/visual-technology/graphics-overview.html
- Vivante GPUs https://en.wikipedia.org/wiki/Vivante_Corporation

- [Unity - Mobile Hardware Stats](http://hwstats.unity3d.com/mobile/gpu.html)
- [Steam Hardware & Software Survey](http://store.steampowered.com/hwsurvey/videocard/)
- [Firefox Hardware Report](https://metrics.mozilla.com/firefox-hardware-report/#detail-pc-video-card)
- https://en.wikipedia.org/wiki/Graphics_processing_unit
- [Category:Graphics processing units — Wikipedia](https://en.wikipedia.org/wiki/Category:Graphics_processing_units)
- [Category:Graphics hardware companies — Wikipedia](https://en.wikipedia.org/wiki/Category:Graphics_hardware_companies)
- [3 Best Practices for Texture Maps on Fire Tablets - Amazon Mobile App Distribution Blog](https://developer.amazon.com/public/community/post/Tx2338FNVTJNJSE/3-Best-Practices-for-Texture-Maps-on-Fire-Tablets)
- [Device and Feature Specifications - Amazon Apps & Services Developer Portal](https://developer.amazon.com/public/solutions/devices/fire-tablets/specifications/01-device-and-feature-specifications)
- [Motorola Developer Resources](http://www-uat.motorola.com/sites/motodev/library/understanding_texture_compression.html)
- [Texture compression tips for Sony Ericsson’s Xperia™ phones – Developer World](http://developer.sonymobile.com/2011/06/21/texture-compression-tips-for-sony-ericssons-xperia-phones/)
- Details about what format supported [Solved: \[WebGL\] Texture compression - BlackBerry Support Community Forums](https://supportforums.blackberry.com/t5/Web-and-WebWorks-Development/WebGL-Texture-compression/td-p/2563217)
- List of device and supported formats [Horn - Compatible Devices for APKs – Humble Bundle](https://support.humblebundle.com/hc/en-us/articles/202954674-Horn-Compatible-Devices-for-APKs-)
- List of devies and their details [GFXBench - unified graphics benchmark based on DXBenchmark (DirectX) and GLBenchmark (OpenGL ES)](https://gfxbench.com/result.jsp)
- Example of device use Adreno GPUs [Adreno GPU SDK - GPU - Qualcomm Developer Network](https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu)
- [Google I/O: Qualcomm Celebrates Launch of Adreno 420 GPU for Android Gaming](http://www.anandtech.com/show/8194/google-io-qualcomm-celebrates-launch-of-adreno-420-gpu-for-android-gaming)
- http://download.nvidia.com/developer/OpenGL_Texture_Formats/nv_ogl_texture_formats.pdf http://download.nvidia.com/developer/OpenGL_Texture_Formats/nv_ogl_texture_formats.xls


## Tools

See https://www.adobe.com/fr/products/gaming-sdk.html

[Independent hardware vendor (IHV)](https://en.wikipedia.org/wiki/Independent_hardware_vendor) and others compressors

- https://github.com/GameTechDev/ISPCTextureCompressor BC6H, BC7, ETC1 and ASTC
	https://software.intel.com/en-us/articles/fast-ispc-texture-compressor-update
- [Intel® Texture Works Plugin for Photoshop* | Intel® Software](https://software.intel.com/en-us/articles/intel-texture-works-plugin), https://github.com/GameTechDev/Intel-Texture-Works-Plugin http://gametechdev.github.io/Intel-Texture-Works-Plugin/ BC1, BC1_SRGB, BC3, BC3_SRGB, BC6H_FAST, BC6H_FINE,BC7_FAST, BC7_FINE, BC7_SRGB_FAST, BC7_SRGB_FINE, BC4, BC5, NONE
- [Compressonator - AMD](https://github.com/GPUOpen-Tools/Compressonator) ASTC, DDS, EXR, KTX, TGA; DXT1, DXT3, DXT5, DXT5_xGBR, DXT5_RxBG, DXT5_RBxG, DXT5_xRBG, DXT5_RGxB, DXT5_xGxR, ATI1N, ATI2N, ATI2N/ATI2N_XY, ATI2N_DXT5, ATC_RGB, ATC_RGBA_Explicit, ATC_RGBA_Interpolated, ETC_RGB, ETC2_RGB, BC6H, BC7, ASTC, GT
	See [Compressonator - GPUOpen](http://gpuopen.com/gaming-product/compressonator/)

	Use it (2.3.2953+) with Wine (1.8+):
	Require winetrick "C++ runtime Libraries" `vcrun2015`. CLI require DLLs from GUI (in same folder)
	Need to add DLL override `api-ms-win-crt-time-l1-1-0` (use native first). See winecfg

	```sh
	CompressonatorCLI.exe -nomipmap -fd DXT5 image.png image_dxt5.dds
	CompressonatorCLI.exe -nomipmap -fd ATC_RGBA_Explicit image.png image_atca.dds
	```

	Note: ATC codec incorrectly swizzling R and B channels (BGR instead of RGB): https://github.com/GPUOpen-Tools/Compressonator/issues/19
	To fix that you can use ImageMagick:

	```sh
	convert image.png -channel rgba -alpha on -set colorspace RGB -separate -swap 0,2 -combine -define png:color-type=6 image_bgra.png
	```
- [NVIDIA Texture Tools](https://github.com/castano/nvidia-texture-tools) DXT1, DXT5, BPTC See also https://github.com/floooh/nvidia-texture-tools (and all potential fork)
	Based on libsquish (see [S3TC - DXT](S3TC - DXT))
	- [GPU Accelerated Texture Compression | NVIDIA Developer](https://developer.nvidia.com/gpu-accelerated-texture-compression)
- [A fast texture compressor for various formats](https://github.com/GammaUNC/FasTC): PNG, KTX, ASTC, BPTC, ETC1, DXT1, DXT5, PVRTC version 1 4BPP RGBA
	For S3TC/DXT, use https://github.com/nothings/stb/blob/master/stb_dxt.h
	See `/build/CLTool/tc`
- (Viewer) [PixelAndPolygon](http://pixelandpolygon.com/) RGB8, RGBA8, BGR8, Depth, RGBA16, RGB32F, HDR, BC7, R11_EAC, RGB8_ETC2, RGBA_BPTC
- https://github.com/hglm/texgenpack based on detex (see detex)
- [Adreno Texture Compression and Visualization Tool](https://developer.qualcomm.com/software/adéreno-gpu-sdk/tools): 3Dc (single-component and two-component), ASTC (LDR and HDR), ATC RGBA (explicit, interpolated), EAC (single-component and two-component), ETC1 RGB8, ETC2 (RGBA8, RGB8, RGB8 Punchthrough Alpha), S3TC (DXT1 RGBA, DXT3 RGBA, DXT5 RGBA)

	Note: in SDK v5.0 the FOURCC of ATC is incorrect for ATC Interpolated and ATC Explicit (ATCI and ATCA are inversed):

	- [Texture Tool does not code FOURCC code correctly in DDS files - Qualcomm Developer Network](https://developer.qualcomm.com/forum/qdevnet-forums/mobile-gaming-graphics-optimization-adreno/26480)
	- [Adreno Texture Tool's bug? (in AdrenoSDK 3.0) - Qualcomm Developer Network](https://developer.qualcomm.com/forum/qdevnet-forums/mobile-gaming-graphics-optimization-adreno/18926)
	- `Adreno SDK/Docs/QCompress/QCompress.pdf` "Developer Notes"

	`QCompress` (Adreno Texture Tool) is GUI only. For CLI command, create you own with TextureConverter lib included in the SDK

	Note: An other existing bug:

	- [KTX swap Red Channel and Blue Channel in Adreno Texture tool - Qualcomm Developer Network](https://developer.qualcomm.com/forum/qdevnet-forums/mobile-gaming-graphics-optimization-adreno/14993)
- [Mali GPU Texture Compression Tool - Mali Developer Center](http://malideveloper.arm.com/resources/tools/mali-gpu-texture-compression-tool/) ASTC, ETC1, ETC2 / EAC (Java Application)
- Lib (see texgenpack) [Low-level library for decompression and manipulation of texture blocks compressed](https://github.com/hglm/detex) KTX, DDS, BC1/DXT1/S3TC, BC2-BC3, BC4/RGTC1, BC5/RGTC2, BC6 (BPTC_FLOAT), BC7 (BPTC), ETC1/2
- Skia lib write/read https://skia.googlesource.com/skia and https://github.com/google/skia PKM, ARTC, KTX, LATC, R11_EAC, ETC1
- ImageMagick module [Texture compress modules for ImageMagick](https://github.com/Perlmint/MagickCompress) PKM, ETC1, pvrtc-4bpp-rgb, pvrtc-4bpp-rgba
- [PVRTexTool - Imagination Community](https://community.imgtec.com/developers/powervr/tools/pvrtextool/) PVR (v3, v2 with `-pvrlegacy`); PVRTC, ETC1-2, EAC, ASTC, DXT
	- [Download the PowerVR Tools and SDK - Imagination](https://www.imgtec.com/developers/powervr-sdk-tools/installers/)
	https://community.imgtec.com/developers/powervr/offline-installers/
	http://cdn.imgtec.com/sdk/PVRTexTool.xml
	Old version of SDK 2.X can generate DXT included in IGEP DSP GST Framework: https://www.isee.biz/support/downloads/item/igep-dsp-gst-framework http://downloads.isee.biz/pub/files/igep-dsp-gst-framework-3_40_00/Graphics_SDK_4_05_00_03/GFX_Linux_SDK/OVG/SDKPackage/Utilities/PVRTexTool/
	See [PowerVR Downloads - Imagination Community](https://community.imgtec.com/developers/powervr/installers/)
	See [PVRTexTool - PVRTexTool.User+Manual.pdf](http://cdn.imgtec.com/sdk-documentation/PVRTexTool.User+Manual.pdf#29)
	PVRTexLib usage examples: https://github.com/TermiT/mkpack https://github.com/KTXSoftware/kraffiti-pvrtc

	```sh
	/Applications/Imagination/PowerVR_Graphics/PowerVR_Tools/PVRTexTool/CLI/OSX_x86/PVRTexToolCLI -m -flip y,flag -f PVRTC1_4  -q pvrtcbest -i image.png
	/Applications/Imagination/PowerVR_Graphics/PowerVR_Tools/PVRTexTool/CLI/OSX_x86/PVRTexToolCLI -i atlas.png -o atlas.pvr -m -l -f PVRTC1_4 -q pvrtcbest -mfilter cubic
	```
- Apple Texturetool KTX, PVR (v2); ASTC, PVRTC 2-4bpp v1
	For PVRTC, use PVRTexTool instead (quicker and better results)
	- [Using texturetool to Compress Textures](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/TextureTool/TextureTool.html)
	- [Technical Q&A QA1611: Creating textures in the PVRTC compression format](https://developer.apple.com/library/ios/qa/qa1611/_index.html)

	```sh
	/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/texturetool -e ASTC --compression-mode-exhaustive --bits-per-pixel-4 -f PVR -o image.pvr image.png
	/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/texturetool -e PVRTC --channel-weighting-perceptual -f PVR -o image.pvrtc image.png
	```
- DirectXTex library read/write DDS and WIC https://github.com/Microsoft/DirectXTex
- Read DSS and PVR https://github.com/toji/texture-tester/blob/master/js/webgl-texture-util.js and https://github.com/pixijs/pixi-compressed-textures/blob/master/src/CompressedImage.js
- Read KTX, PKM, DDS, ASTC, PVR https://bitbucket.org/rude/love/src/9d8164a7e6b3/src/modules/image/magpie/
- Read ATT, PVRTC, http://sio2interactive.forumotion.net/t134-compressed-textures-from-apple-s-texturetool
- Read PVR, DDS PXC, PPM, etc. https://sourceforge.net/p/irrlicht/code/HEAD/tree/trunk/source/Irrlicht/
- Write DDS, ETC1, ETC2, PVR https://github.com/paulvortex/RwgTex use other lib/tools like Gimp DDS plugin, Nvidia DXTlib, Crunch lib, ETCPack, Compressonator, NVidia Texture tools compressor, Imagination PowerVR SDK TexTool, Rg-ETC1
- Read DDS, PVR, decompress PVRTC (use PowerVR SDK PVRTDecompress) https://github.com/sergeyreznik/et-engine/tree/metal_integration/include/et/imaging
- Read DDS, PVR https://github.com/DrDrake/mcore3d/tree/master/MCD/Loader
- Read and write DDS, KMG, KTX https://github.com/g-truc/gli
