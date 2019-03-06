See [LZ77](Algorithms#lz77)

- [Compressor Head - YouTube](https://www.youtube.com/playlist?list=PLOU2XLYxmsIJGErt5rrCqaSGTMyyqNt2H) - Well explained videos about compression (how to compression works, how to write a compression algorithms) by Colt McAnlis.
	- Variable Length Codes
	- The LZ77 Compression Family
	- Markov Chains
	- Burrows-Wheeler transform
	- Arithmetic Compression
	- Adaptive Statistical Encoding

## Exploits

All compressions are subject to decompression bomb.

See:

- [Deflate Decompression Bomb](Deflate#decompression-bomb)
- [ZIP Decompression Bomb](ZIP#decompression-bomb)
- [AERAsec - Network Security - Eigene Advisories](http://www.aerasec.de/security/advisories/decompression-bomb-vulnerability.html)

## Optimization

Content optimization for compression

Sometime an optimized content will produce larger compressed version than the non optimized (GZIP threshold)

- [Of SVG, Minification and Gzip – Noteworthy — The Journal Blog](https://blog.usejournal.com/of-svg-minification-and-gzip-21cd26a5d007)
- [CSS Compression : Minifier Roulette](http://mainroach.blogspot.fr/2013/07/css-compression-minifier-roulette.html)
