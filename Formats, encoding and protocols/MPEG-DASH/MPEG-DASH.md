- [Dynamic Adaptive Streaming over HTTP — Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP)
- [MPEG DASH validator JS library](https://github.com/Eyevinn/dash-validator-js)
- [WebM Dash Specification - wiki](http://wiki.webmproject.org/adaptive-streaming/webm-dash-specification) - WebM DASH
- [axiomatic-systems/Bento4: Full-featured MP4 format and MPEG DASH library and tools](https://github.com/axiomatic-systems/Bento4)

Translate a fMP4 m3u8 manifest into a DASH manifest

For DASH main profile (using segment lists):

	MP4Box -mpd source.m3u8

For DASH live profile (using segment template):

	MP4Box -use-template -mpd source.m3u8

Similar technologies:

HTTP Live Streaming aka HLS:

- [Introduction](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/Introduction/Introduction.html)
- [HTTP Live Streaming — Wikipedia](https://en.wikipedia.org/wiki/HTTP_Live_Streaming)
- [Deploying HTTP Live Streaming](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/DeployingHTTPLiveStreaming/DeployingHTTPLiveStreaming.html)
- [Technical Note TN2288: Example Playlist Files for use with HTTP Live Streaming](https://developer.apple.com/library/content/technotes/tn2288/_index.html) - (in segments playlist) "Important: The `EXT-X-ENDLIST` tag is not present in the Live playlist, indicating that new media files will be added to the index file as they become available."
- [HTTP Live Streaming Examples - Apple Developer](https://developer.apple.com/streaming/examples/)
- [video-dev/hls.js: JavaScript HLS client using Media Source Extension](https://github.com/video-dev/hls.js)
- [HTTP Live Streaming (HLS) - Apple Developer](https://developer.apple.com/streaming/)
- can use fragmented MP4, aka fMP4: multi-segment mp4 or single-segment mp4

fmp4 segments playlist:

	#EXTM3U
	#EXT-X-TARGETDURATION:6
	#EXT-X-VERSION:7
	#EXT-X-MEDIA-SEQUENCE:1
	#EXT-X-PLAYLIST-TYPE:VOD
	#EXT-X-INDEPENDENT-SEGMENTS
	#EXT-X-MAP:URI="main.mp4",BYTERANGE="721@0"
	#EXTINF:6.00000,	
	#EXT-X-BYTERANGE:5874288@721
	main.mp4
	#EXTINF:6.00000,	
	#EXT-X-BYTERANGE:5863101@5875009
	main.mp4
	#EXTINF:6.00000,	
	#EXT-X-BYTERANGE:5856476@11738110
	main.mp4
	#...
