DirectDraw Surface (DDS)

Texture container. Can contains multiple levels (mipmap) encoded with S3TC/DXT and ATC, etc.

`image/vnd-ms.dds`

- [Multimedia Formats and Tools - PS3 Developer wiki](http://www.psdevwiki.com/ps3/Multimedia_Formats_and_Tools#DDS)

## Input

- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osgPlugins/dds/ReaderWriterDDS.cpp
- Libav read DDS https://github.com/libav/libav/blob/ab3554e1a7c04a5ea30f9c905de92348478ef7c8/libavcodec/dds.c
- DevIL https://github.com/DentonW/DevIL/blob/master/DevIL/src-IL/include/il_dds.h https://github.com/DentonW/DevIL/blob/master/DevIL/src-IL/src/il_dds.c
- [Texture rendering problem for ATITC Textures - Qualcomm Developer Network](https://developer.qualcomm.com/comment/4509#comment-4509)

## Output

See [Texture format](../Texture%20format/Texture%20format.md)

- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osgPlugins/dds/ReaderWriterDDS.cpp
- [Download DirectX Software Development Kit from Official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=6812)
- DirectXTK https://github.com/Microsoft/DirectXTK/blob/master/Src/DDSTextureLoader.cpp https://github.com/Microsoft/DirectXTK/blob/master/Src/XboxDDSTextureLoader.cpp https://github.com/Microsoft/DirectXTK/blob/master/Src/dds.h
- DirectXTex
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/gimp-dds/)
- DevIL https://github.com/DentonW/DevIL/blob/master/DevIL/src-IL/include/il_dds.h https://github.com/DentonW/DevIL/blob/master/DevIL/src-IL/src/il_dds-save.c

### ImageMagic

ImageMagic as parameter `dds:mipmaps` but it's dont match DDS format value: always to 1, means one (default) level, use 0 to disable mipmap generation.

```sh
convert image_rgba.png -format dds -define dds:compression=dxt5 -define dds:cluster-fit=true -define dds:mipmaps=0 image_rgba_dxt5.dds
```

- (about ImageMagic `dds:mipmaps` option) [Strange "add" behaviour - Page 2 - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?f=1&t=23946&start=15#p102687)
- (about ImageMagic DDS specific options) [Strange "add" behaviour - Page 2 - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?f=1&t=23946&start=15#p102574)

- http://trac.openscenegraph.org/projects/osg/browser/OpenSceneGraph/branches/OpenSceneGraph-3.0/src/osgPlugins/dds/ReaderWriterDDS.cpp
