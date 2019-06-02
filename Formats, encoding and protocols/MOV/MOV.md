- [A library for writing file metadata in ActionScript3](https://github.com/benstucki/metaphile)
- [Codec Central - QuickTime](https://www.siggraph.org/education/materials/HyperGraph/video/architectures/QuickTime.html) - (old) Codecs QuickTime supports
- [Media Data Atom Types](https://developer.apple.com/library/content/documentation/QuickTime/QTFF/QTFFChap3/qtff3.html#//apple_ref/doc/uid/TP40000939-CH205-74522) - (Video) image compression formats
- [FFmpeg/mov.c at master · FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg/blob/master/libavformat/mov.c)
- [Libquicktime homepage](http://libquicktime.sourceforge.net/introduction.html) - [Libquicktime download | SourceForge.net](https://sourceforge.net/projects/libquicktime/)

## QuickTime VR

QTVR object or QTVR panorama

`vrsg` atom type

- [Media Data Atom Types](https://developer.apple.com/library/content/documentation/QuickTime/QTFF/QTFFChap3/qtff3.html#//apple_ref/doc/uid/TP40000939-CH205-69877) - QuickTime VR world / QTVR
- [Summary of VR World and Node Atom Types](https://developer.apple.com/library/content/documentation/QuickTime/QTFF/QTFFChap3/qtff3.html#//apple_ref/doc/uid/TP40000939-CH205-57980)
- [QuickTime VR — Wikipedia](https://en.wikipedia.org/wiki/QuickTime_VR)
- [FreePV download | SourceForge.net](https://sourceforge.net/projects/freepv/)
- [Panorama, virtual tour and 3D object movies created by Easypano software](http://www.easypano.com/panorama-virtual-tour/gallery.html), [QuickTime VR panorama software and QuickTime VR 3D object movie software](http://www.easypano.com/qtvr.html), [Panorama Gallery - Panoramic Image - Panoramic Photo](http://www.easypano.com/panorama-gallery.html)
- [Tutorial 15 | How to make a Quicktime VR Object on Vimeo](https://vimeo.com/57657461)
- [Dr. Lex' QTVR Panoramas and Objects](https://www.dr-lex.be/info-stuff/qtvr.html), [The Technology Behind QTVR](https://www.dr-lex.be/info-stuff/qtvrmath.html)
- [CuTy | fieldOfView](http://fieldofview.com/projects/cuty) - [fieldOfView/CuTy: a QTVR viewer based on Flash 10](https://github.com/fieldOfView/CuTy). See also [QTVR Examples | PanoPress](http://www.panopress.org/example/qtvr-examples/)
- [QuicktimeVR parser | fieldOfView | SPi-V dev](http://legacy.fieldofview.com/spv-dev/projects/qtparser)
- [krpano.com](https://krpano.com/) - need decompile protected flash code

Cinema 4D can export to "QuickTime VR Object" (in Render Settings)

## Fast start

To speed up loading or streaming, metadata should be at the begining:

	[ 'mdat' QT data atom ]+[ 'moov' QT info atom ] to [ 'moov' QT info atom ]+[ 'mdat' QT data atom ]

	ffmpeg -i simple1.mp4 -codec copy -map 0 -movflags +faststart output.mp4
	qt-faststart <infile.mov> <outfile.mov>

- [Encode/H.264 – FFmpeg](https://trac.ffmpeg.org/wiki/Encode/H.264#faststartforwebvideo)
