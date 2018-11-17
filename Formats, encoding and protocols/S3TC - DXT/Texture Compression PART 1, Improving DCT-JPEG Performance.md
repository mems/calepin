# Texture Compression PART 1, Improving DCT/JPEG Performance

http://www.sebbylive.com/2011/07/20/texture-compression-part-1

In the first phase of my project, I decided to see if there were possible ways to improve JPEG-like texture compression scheme (such as used in [ID's Tech 5 Virtual Texture system](http://en.wikipedia.org/wiki/Id_Tech_5)) by taking advantage of the fact that the texture will be transcoded into a [DXTC format](http://en.wikipedia.org/wiki/S3_Texture_Compression), which is also lossy in nature. I have done some experimenting and thought I would share the results I found so far. The basic idea/approach is simple, knowing that the DXTC format is lossy can we dynamically adjust the DCT quantization in order to improve compression. The assumption is that knowing what the two colors assigned to a DXTC block are know and passed on to the decoder, can we compress the remaining colors more, as long as they remain the same once transcoded to DXTC. The approach is simple, but the implementation of such a test isn't as straightforward. For my tests, I used <a href="/web/20121228104422/http://code.google.com/p/libsquish/" target="_blank">Squish </a>as my DXTC compression library. For the JPEG/DCT compressor, I opted to use the <a href="/web/20121228104422/http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB4QFjAA&url=http%3A%2F%2Fsoftware.intel.com%2Fen-us%2Farticles%2Fintel-ipp%2F&ei=oaQlTuCzGfLXiALAsp3wCQ&usg=AFQjCNHhKtx8RepzsoHHxjL-aroM8ZOZOQ" target="_blank">Intel IPP libraries</a> as I could assemble the needed pieces of a basic DCT compressor without having to worry about breaking down a more complex JPEG implementation to meet my needs.

NOTE: At this point, I have only implemented the DCT transform and Quantization of the encoder. I am not focusing on the actual compressed size but want to at least test my initial theory to see if different compression levels per block can be achieved with knowledge about how the original image is compressed in DXTC form.

To keep the UI aspect of the application simple, I've built the code using C# which makes the display of images and just the general framework easier to maintain. The core compression functionality however is done in a Managed C++ library and I expose the few basic API calls needed to the C# application. The application takes care of loading the images and grabbing a copy of the RGB data. The first function I implemented was a simple DXTC compress/decompress routine which, based on a supplied image, returns the DXTC decompressed version of this image. Here is the code from this function:

	void Comp::DXT_CompressDecompress(Ipp8u* srcData, int stride, int width, int height, Ipp8u* dstData, int dstStride)
	{
		Ipp8u rawDXTCColors[4 * 4 * 4];
		Ipp8u decompDXTCColors[4 * 4 * 4];
		Ipp16u compDXTCColors[4];
		
		Ipp16u blockIndex = 0;
		
		for(int y=0; y<(height/4); y++)
		{
			for(int x=0; x<(width/4); x++, blockIndex++)
			{
				Ipp32u srcOffset = (x * 4 * 3) + (y * 4 * stride * 3);
				Ipp32u dstOffset = (x * 4 * 3) + (y * 4 * dstStride * 3);
				IppiSize roiSize = {4, 4};
				
				// Compress image.
				Ipp8u defaultColor[4] = {255, 255, 255, 255};
				ippiSet_8u_C4R(defaultColor, rawDXTCColors, 16, roiSize);
				ippiCopy_8u_C3AC4R( srcData + srcOffset, stride * 3, rawDXTCColors, 16, roiSize );
				squish::Compress(rawDXTCColors, compDXTCColors, squish::kDxt1);
				
				// Decompress Image.
				squish::Decompress(decompDXTCColors, compDXTCColors, squish::kDxt1);
				ippiCopy_8u_AC4C3R(decompDXTCColors, 16, dstData + dstOffset, dstStride * 3, roiSize );
			}
		}
	}

I also implemented a similar function which did a basic DCT compression decompression based on a provided quantization table. The function does not do any entropy coding as the goal was not to determine the size of the compressed texture at this point but only to recover the resulting image from the compression process. It turns out this is fairly simple with the Intel IPP once you get a feel for the API:

	void Comp::DCT_CompressDecompress(Ipp8u* srcData, int stride, Ipp16u* pQuantFwdTable, Ipp16u* pQuantInvTable)
	{
		// CSC and downsample to JPEG Friendly MCUs
		Ipp16s dxtMCUY[8 * 8 * 4];
		Ipp16s dxtMCUCb[8 * 8];
		Ipp16s dxtMCUCr[8 * 8];
		Ipp16s* dxtMCU[3] = {dxtMCUY, dxtMCUCb, dxtMCUCr};
		ippiRGBToYCbCr411LS_MCU_8u16s_C3P3R(srcData, stride * 3, dxtMCU);
		
		// Process Cr channel
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUCr, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUCr, pQuantInvTable);
		
		// Process Cb channel
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUCb, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUCb, pQuantInvTable);
		
		// Process Y channel
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUY, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUY, pQuantInvTable);
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUY + 64, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUY + 64, pQuantInvTable);
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUY + 128, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUY + 128, pQuantInvTable);
		ippiDCTQuantFwd8x8_JPEG_16s_C1I(dxtMCUY + 192, pQuantFwdTable);
		ippiDCTQuantInv8x8_JPEG_16s_C1I(dxtMCUY + 192, pQuantInvTable);
		
		// Reverse CSC to recover initial image
		ippiYCbCr411ToRGBLS_MCU_16s8u_P3C3R((const Ipp16s**)dxtMCU, srcData, stride * 3);
	}

In my first experiment, I decided to simply compress the blocks as is through DCT at different quantization levels. Once decompressed, I would run the results through the DXT compressor and see at which quantization level the results would start to diverge. Ultimately, the idea is to determine the two DXT colors per block and transmit them separately. Then the block colors would be compressed with the highest quantization that would yield the same selector bits. In other words, we would compress as much as we can until the color drift enough to fall in a different DXT bucket. But I started with the simpler experiment to give me a feel as to whether or not the idea would work (the full implementation being significantly more time consuming).

All the tests I have run so far have had disappointing results. Even at high DCT quality levels, the DXTC selector bits start deviating from the selector bits of the original image. Obviously, compressing the block as a whole is far from ideal, since it does also change the colors used in the process of determining the DXTC endpoint colors. However, this does make me realized that even for the second experiment, this may give some problems.

Simply put, if a color happens to lay near the edge between two selector bits, it will take little DCT error to cause the color to jump into the next bucket. So I cannot purely do a simple bit compare but also need to take in consideration how much deviation there is within DCT compression to weed out cases where the bit changes were due to proximity to the neighboring selector. This sure makes the complex implementation already more complex.

On the bright side, this makes me think of another possibly simpler approach. Instead of trying to find a perfect match, we could use the result of the DXT compression as a noise level basis to determine the noise level introduced by the DCT compression. This could be used as a rate control mechanism, assuming a decent perceptual error metric, to ensure the bits are optimally distributed within the DCT compressed image.

Moving on to the next part of the experimentation, I am still considering the selector bit comparison approach but will also look into possible error metrics which could make a rate control mechanism viable.