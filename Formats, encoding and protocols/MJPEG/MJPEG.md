Sometimes called MJPG.

Demo RTP streams:

- http://173.14.66.201/anony/mjpg.cgi Northgate Launder Land
- list [TTrix](http://www.ttrix.com/apple/iphone/ipvision/ipvisionpubcameras.html)
- http://cam.butovonet.ru/mjpg/video.mjpg
- http://user:allesfrisch.99@62.68.193.82:8002/mjpg/video.mjpg
- http://gccvideo.dynalias.com/mjpg/video.mjpg?camera=1
- http://80.32.204.149:8080/mjpg/video.mjpg?camera=1
- http://195.67.26.73/mjpg/video.mjpg?camera=1
- http://96.10.1.168/view/view.shtml?id=1149614&imagepath=%2Fmjpg%2F1%2Fvideo.mjpg&size=1

Used by IP cameras, Digital cameras

- [Is the 1Dx mkII MJEPG \<b\>bad codec</b>? | Pixla's blog](http://pixla.ch/blog/files/canonmjpeg422codec.php)

File storage:

No official container. Non official can be AVI or MOV based where frame data is a JPEG file
Each frames start with 0xffd8ff (JPEG magick number)
> A single frame of MJPEG video may or may not contain the associated JPEG Huffman tables.
> For QuickTime formats, Apple has defined two types of coding: MJPEG-A and MJPEG-B. MJPEG-B no longer retains valid JPEG Interchange Files
An other way is to store as HTTP stream without first headers (before first boundary) see https://github.com/waveform80/picamera/issues/335
An other way is to store all JPEG frames concatenated in one file 

HTTP stream (multipart message):

	Content-Type: multipart/x-mixed-replace;boundary=xxboundaryxx
	
	--xxboundaryxx
	
	Content-Type: image/jpeg
	Content-Length: 1000
	
	JIFFdata..frame1.1000
	
	--xxboundaryxx
	
	Content-Type: image/jpeg
	Content-Length: 1000
	
	JIFFdata..frame2.1000
	
	--xxboundaryxx
	

Additional headers can be used to discard browser cache:

	Connection: keep-alive
	Cache-Control: no-cache, no-store, must-revalidate
	Pragma: no-cache
	Expires: 0

- [RFC 2435 - RTP Payload Format for JPEG-compressed Video](https://tools.ietf.org/html/rfc2435)
- [Motion JPEG — Wikipedia](https://en.wikipedia.org/wiki/Motion_JPEG)
- [actionscript 3 - What is the specifications for Motion JPEG? - Stack Overflow](https://stackoverflow.com/questions/885160/what-is-the-specifications-for-motion-jpeg)
- [Development and Implementation of an MotionJPEG Capable JPEG Decoder in Hardware - websvn,filedetails](http://opencores.org/websvn,filedetails?repname=mjpeg-decoder&path=%2Fmjpeg-decoder%2Ftrunk%2Fmjpeg.pdf#page=43)
- https://bugs.chromium.org/p/chromium/issues/detail?id=308999
- [How To Convert MJPEG Compressor IMediaSamples To .JPG ??](https://social.msdn.microsoft.com/Forums/windowsdesktop/en-US/f606b498-f6f1-4565-91b2-d623350f364d/how-to-convert-mjpeg-compressor-imediasamples-to-jpg-)
- [MJPEG (Motion JPEG) Video Codec](http://www.digitalpreservation.gov/formats/fdd/fdd000063.shtml)
- [Motion JPEG File Format](http://forums.codeguru.com/showthread.php?173230-Motion-JPEG-File-Format)
- [Photo JPEG vs Motion JPEG A vs Motion JPEG B](http://lists.apple.com/archives/quicktime-talk/2000/Nov/msg00269.html)
- [JPEG image compression FAQ, part 1/2Section - \[20\] Isn't there an M-JPEG standard for motion pictures?](http://www.faqs.org/faqs/jpeg-faq/part1/section-20.html)
- "An MJPEG variant with data rearranged in a slightly unusual manner [...] used by the software for Aiptek MegaCam" https://wiki.multimedia.cx/index.php?title=Sunplus_JPEG
- [Motion JPEG - MultimediaWiki](https://wiki.multimedia.cx/index.php/Motion_JPEG)

See also

- [Motion JPEG 2000 — Wikipedia](https://en.wikipedia.org/wiki/Motion_JPEG_2000)
- [AMV video format — Wikipedia](https://en.wikipedia.org/wiki/AMV_video_format)

Tools and libs

- `ffmpeg` with `-f mjpeg` or `-vcodec mjpeg` `ffmpeg -i in.avi -y out.mjpeg` `ffmpeg -i mjpegvideo.avi -vcodec copy frame%d.jpg`
- [MJPEG Tools](http://mjpeg.sourceforge.net/)
- [MJPG-streamer download | SourceForge.net](https://sourceforge.net/projects/mjpg-streamer/) see https://sourceforge.net/p/mjpg-streamer/code/HEAD/tree/mjpg-streamer/plugins/output_http/httpd.c
- [This jQuery plugin provides a simple player for MJPEG ("motion JPEG") videos](https://github.com/clipchamp/jquery-clipchamp-mjpeg-player-plugin)
- http://ushiroad.com/mjpeg/js/lib/mjbuilder.js

From VLC sources:

- `VLC_CODEC_MJPG` and `MFVideoFormat_MJPG`
- https://github.com/videolan/vlc/blob/fbaa27ae2d7fcf5ccee7f0ca424ec0cc5bf01f4c/modules/access/v4l2/linux/videodev2.h#L580
- https://github.com/videolan/vlc/blob/fbaa27ae2d7fcf5ccee7f0ca424ec0cc5bf01f4c/modules/demux/mjpeg.c
- https://github.com/videolan/vlc/blob/fbaa27ae2d7fcf5ccee7f0ca424ec0cc5bf01f4c/modules/mux/mpjpeg.c
- https://github.com/videolan/vlc/blob/7f4fa0414e6421fef7ac884f7a28ef0bbc03e956/modules/demux/mkv/matroska_segment_parse.cpp#L1421-L1423
- https://github.com/videolan/vlc/blob/46b6e7af7640bc827a37c482948cf8de7034b57c/modules/mux/mp4/libmp4mux.c#L1116
- https://github.com/videolan/vlc/blob/fb9ba9cbb37a56b7e4ee401d50380cfb3d6dca2e/modules/demux/mp4/essetup.c#L531-L533
- https://github.com/videolan/vlc/blob/fbaa27ae2d7fcf5ccee7f0ca424ec0cc5bf01f4c/modules/mux/ogg.c#L396
- https://github.com/videolan/vlc/blob/df5663381bb7b54dc1b6b4e38d541f246de9ba45/modules/access/live555.cpp#L1074-L1077

From ffmpeg sources:

- https://github.com/FFmpeg/FFmpeg/blob/c493a531edfd7b6956c563e19eb3a851b76797de/doc/bitstream_filters.texi#L129-L170
- https://github.com/FFmpeg/FFmpeg/tree/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavcodec/mjpeg*
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavcodec/vaapi_encode_mjpeg.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavcodec/jpegtables.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavcodec/sp5xdec.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/rtpenc_jpeg.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/ingenientdec.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavcodec/ljpegenc.c
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/rawdec.c#L125-L190
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/rtpdec_jpeg.c
- https://github.com/FFmpeg/FFmpeg/blob/6d09d6edbc464454a620e3ecf64fe752b5cfa9cc/libavformat/riff.c#L180-L212
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/smjpeg.c
- https://github.com/FFmpeg/FFmpeg/blob/2343f23e4d7e0d0f6adfd83d7d769a7a115dbd17/libavformat/matroska.c#L79
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/swfenc.c#L214
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavformat/rtp.c#L61
- https://github.com/FFmpeg/FFmpeg/blob/415f907ce8dcca87c9e7cfdc954b92df399d3d80/libavdevice/vfwcap.c#L87-L90
- https://github.com/FFmpeg/FFmpeg/blob/73651090ca1183f37753ee30a7e206ca4fb9f4f0/libavcodec/codec_desc.c#L86-L100