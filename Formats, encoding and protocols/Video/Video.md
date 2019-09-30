- [Enhance detail](Graphics#enhance-detail)
- [ffdshow tryouts | Official Website](http://ffdshow-tryout.sourceforge.net/)
- [GPAC | Multimedia Open Source Project](https://gpac.wp.imt.fr/)
- [Fabio_Sonnati_Encoding Video for the Highest Quality and Performance_MaxEurope2008.pdf](Fabio_Sonnati_Encoding Video for the Highest Quality and Performance_MaxEurope2008.pdf)
- [Fabio_Sonnati_MAX2010_H.264 Encoding Strategies for all screens_final.pdf](Fabio_Sonnati_MAX2010_H.264 Encoding Strategies for all screens_final.pdf)

temporal compression (base on other frames) vs spatial compression (based only on pixels of the same frame, like a still image)

- [Motion 4 User Manual: Popular Video Codecs for File Exchange](https://documentation.apple.com/en/motion/usermanual/chapter_B_section_3.html)

## Compression and optimisation

Pixel aligned on H.264/AVC which use 16×16 macroblocks (partition size prediction): [Macroblock — Wikipedia](https://en.wikipedia.org/wiki/Macroblock) (Other sizes can be choose 16×8, 8×8, 8×4, 4×4)

- [Video Optimization – A matter of Adaptivity | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2016/05/04/video-optimization-a-matter-of-adaptivity/)
- [Smart content encoding at VEVO](http://blog.vevo.com/smart-content-encoding-at-vevo/) - How to choose video size + bitrate: make stats

### GPU texture codec

- [Texture format](../Texture%20format/Texture%20format.md)
- [BinomialLLC/basis_universal: Basis Universal GPU Texture Codec](https://github.com/BinomialLLC/basis_universal)

## Frame types

[APNG](PNG#apng) use one one I-Frame + P‑frame (base on the I-Frame only) with blend mode

To get frames infos:

- `ffmpeg -i video.mp4 -vstats_file stats.txt -f null - >/dev/null && awk '/type= I/ {print $2}' stats.txt`
- `ffprobe -show_frames test.mp4 > awk -F= ' /pict_type=/ { if (index($2, "I")) { i=1; } else { i=0; } } /coded_picture_number/ { if (i) print $2 } '`

Force I-frames (keyframes):

- [video - What is the CORRECT way to fix keyframes in FFMPEG for DASH? - Super User](https://superuser.com/questions/908280/what-is-the-correct-way-to-fix-keyframes-in-ffmpeg-for-dash)

More infos about frames:

- [mpeg - Setting B frames in a video with ffmpeg - Stack Overflow](https://stackoverflow.com/questions/15855535/setting-b-frames-in-a-video-with-ffmpeg)
- [Video compression picture types — Wikipedia](https://en.wikipedia.org/wiki/Video_compression_picture_types)
- [ffmpeg tutorial](http://dranger.com/ffmpeg/tutorial05.html)

## Alpha

Videos codec often don't support alpha, often used for entertainment or support that dont need alpha channel.

Use a dedicated format like: WebM with codecs: VP8, VP8 or MOV with codecs: PNG (FourCC: `png `), QuickTime None (FourCC: `v408`) or QuickTime Animation (FourCC: `rle `) or FLV/F4V

Or use side by side (or 2 files) for channels (RGB + A) videos. See [Side by side channels](Image#side-by-side-channels)

- Generate a MOV from suite of PNG images and use the PNG codec: `ffmpeg  -i "test.%04d.png" -vcodec copy -y test.mov`
- [Alpha compression](Image#alpha-compression)
- [HTML5 Video with alpha transparency](http://www.sciencelifeny.com/transparency/transparency.html) - Use side by side channels
- [m90/seeThru: HTML5 video with alpha channel transparencies](https://github.com/m90/seeThru) - Use side by side channels
- [tsheaff/TSHAlphaVideos: Play mp4 videos with alpha background on iOS](https://github.com/tsheaff/TSHAlphaVideos)

## Decompression using GPU

### HAP

Use [S3TC texture compression](S3TC - DXT):

- Hap (DXT1) has the lowest data-rate and reasonable image quality.
- Hap Alpha (DXT5) has similar image quality to Hap, and supports an Alpha channel.
- Hap Q (Scaled DXT5-YCoCg) has improved image quality, at the expense of larger file sizes

Support alpha, fast playback (should support both direction)

Supported by FFMPEG, as QuickTime codec (or with any other container format like MP4, MKV, etc.)

	ffmpeg -i test.mp4 -vcodec hap -format hap_q -chunks 8 out.mov
	# 8 chunks for allow 8 thread to decode the video
	# output MOV but could be MP4 too or any other video container format

- [Vidvox/hap: A codec for fast video playback](https://github.com/Vidvox/hap)
- [hap/HapVideoDRAFT.md at master · Vidvox/hap](https://github.com/Vidvox/hap/blob/master/documentation/HapVideoDRAFT.md)
- [Vidvox/hap-qt-codec: A QuickTime codec for Hap video](https://github.com/Vidvox/hap-qt-codec)
- [Presenting Hap, a family of open-source GPU accelerated video codecs — VDMX - MAC VJ SOFTWARE](http://vdmx.vidvox.net/blog/hap)

## Encoded timecode

Render timecode as barcode, used for image synchronization (tracking, etc.)

- [SMPTE timecode — Wikipedia](https://en.wikipedia.org/wiki/SMPTE_timecode)
- [Video Sync Issues with Flash AS3 | Decker Labs](http://blog.edecker.net/2011/08/video-sync-issues-with-flash-as3/)
- [AS3: Perfect video sync with embedded frame numbers « Niko Helle](http://nikohelle.net/2011/11/25/as3-perfect-video-sync-with-embedded-frame-numbers/)

## Audio language

	ffmpeg -i INPUT -metadata:s:a:0 language=eng OUTPUT

- [ffmpeg Documentation](https://ffmpeg.org/ffmpeg.html#Main-options)

## Subtitles

	ffmpeg -i input.mp4 -f srt -i infile.srt -codec copy -c:s mov_text output.mp4 -metadata:s:s:0 language=eng
	ffmpeg -i input.mp4 -codec copy output.mkv -sub_charenc UTF-8 -f srt -i subtitles.srt

- https://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo
- https://stackoverflow.com/questions/8672809/use-ffmpeg-to-add-text-subtitles/33289845#33289845
- [FFMPEG An Intermediate Guide/subtitle options - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/subtitle_options)
- [Subtitles – HandBrake](https://trac.handbrake.fr/wiki/Subtitles)