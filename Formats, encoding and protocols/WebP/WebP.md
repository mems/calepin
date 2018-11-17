Base on VP8 video codec

- `ffmpeg -framerate 15 -i image-%d.png -loop 128 animation.webp`
- [WebPJS](http://webpjs.appspot.com/) (client side decoder lib)
- [cwebp](https://developers.google.com/speed/webp/docs/cwebp) (Compress an image file to a WebP file)
- Black WebP: `pngcrush -force -blacken ; cwebp -lossless -q 90`
- https://github.com/google/skia/blob/fcee51038aeaf3596a4ffcdba0bf18e3155e09b9/src/images/SkWEBPImageEncoder.cpp
- [How WebP works (lossly mode) – Medium](https://medium.com/@duhroach/how-webp-works-lossly-mode-33bd2b1d0670)
- [WebP Gallery  |  WebP  |  Google Developers](https://developers.google.com/speed/webp/gallery1)
- [Lossless and Alpha Gallery  |  WebP  |  Google Developers](https://developers.google.com/speed/webp/gallery2)
- [WebP decoder for Flash. | UnitZeroOne](http://unitzeroone.com/blog/2011/11/20/webp-decoder-for-flash/)
- [FRDX - PNG vs WebP](http://frdx.free.fr/png_vs_webp.htm)
- [A Picture Costs A Thousand Words](http://www.slideshare.net/guypod/a-picture-costs-a-thousand-words18062013/44) - see [A picture costs a thousand words](a-20picture-20costs-20a-20thousand-20words-130619124428-phpapp01.pdf#page=44)
- [antimatter15/whammy: A real time javascript webm encoder based on a canvas hack](https://github.com/antimatter15/whammy) - Convert WebP to WebM (1 frame movie), this allow a browser that support WebM but not WebP to ready it.
- [Essential Image Optimization](https://images.guide/#what-is-webp)