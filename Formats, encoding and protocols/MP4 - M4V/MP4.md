- [MP4Box](https://gpac.wp.mines-telecom.fr/mp4box/) is part of `gpac`
- fragmented MP4 aka fMP4: [media - What exactly is Fragmented mp4(fMP4)? How is it different from normal mp4? - Stack Overflow](https://stackoverflow.com/questions/35177797/what-exactly-is-fragmented-mp4fmp4-how-is-it-different-from-normal-mp4)

## Fast start

To speed up loading or streaming, metadata should be at the begining:

1. 'moov' info atom
2. 'mdat' data atom

Encoder usally output:

1. 'mdat' data atom
2. 'moov' info atom

To fix that:

	ffmpeg -i input.mp4 -codec copy -map 0 -movflags +faststart output.mp4
	qt-faststart input.mp4 output.mp4

- [Encode/H.264 – FFmpeg](https://trac.ffmpeg.org/wiki/Encode/H.264#faststartforwebvideo)
- [Tools to fix MP4 videos so players can start playback instantly (without downloading the whole file) | monline](http://muzso.hu/2012/11/14/tools-to-fix-mp4-videos-so-players-can-start-playback-instantly-without-downloading-the-w)
- [AtomicParsley](http://atomicparsley.sourceforge.net/)
- [Understanding the MPEG-4 movie atom | Adobe Developer Connection](http://www.adobe.com/devnet/video/articles/mp4_movie_atom.html)
- Python version https://github.com/danielgtaylor/qtfaststart
- https://github.com/FFmpeg/FFmpeg/blob/master/tools/qt-faststart.c
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/moovrelocator/) see also issues https://code.google.com/archive/p/moovrelocator/issues
- [Improving qt-faststart | Breaking Eggs And Making Omelettes](https://multimedia.cx/eggs/improving-qt-faststart/)
- [QTIndexSwapper - Renaun Erickson | Renaun Erickson](http://renaun.com/blog/code/qtindexswapper/)
- [QTIndexSwapper 2 - Renaun Erickson | Renaun Erickson](http://renaun.com/blog/2010/06/qtindexswapper-2/)