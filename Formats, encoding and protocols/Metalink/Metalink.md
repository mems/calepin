	Etag: "thvDyvhfIqlvFe+A9MYgxAfm1q5="
	Link: <http://www2.example.com/example.ext>; rel=duplicate
	Link: <ftp://ftp.example.com/example.ext>; rel=duplicate
	Link: <http://example.com/example.ext.torrent>; rel=describedby;
	type="application/x-bittorrent"
	Link: <http://example.com/example.ext.meta4>; rel=describedby;
	type="application/metalink4+xml"
	Link: <http://example.com/example.ext.asc>; rel=describedby;
	type="application/pgp-signature"
	Digest: SHA-256=MWVkMWQxYTRiMzk5MDQ0MzI3NGU5NDEyZTk5OWY1ZGFmNzgyZTJlO
	DYzYjRjYzFhOTlmNTQwYzI2M2QwM2U2MQ==

	<?xml version="1.0"?>
	<metalink xmlns="urn:ietf:params:xml:ns:metalink" version="4.0">
		<file name="file1.jpg"><url>https://example.com/file1.jpg</url></file>
		<file name="file2.png"><url>https://example.com/file2.png</url></file>
	</metalink>

- [RFC 5854 - The Metalink Download Description Format](https://tools.ietf.org/html/rfc5854)
- [RFC 6249 - Metalink/HTTP: Mirrors and Hashes](http://tools.ietf.org/html/rfc6249)
- [Metalinker.org - Bridging the gap](http://www.metalinker.org/)
- [Metalink — Wikipedia](https://en.wikipedia.org/wiki/Metalink)

Tools supports metalink format:

- [JDownloader.org - Official Homepage](http://www.jdownloader.org/)
- [DownThemAll!](http://www.downthemall.net/)
- command line tool [aria2](http://aria2.sourceforge.net/)