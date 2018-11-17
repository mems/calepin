# Improving DXT Compression File Sizes

http://www.sebbylive.com/projects/texture-compression/improving-dxt-compression-file-sizes

This is a little bit of a sidetrack from my previous project postings but is something that I experimented with a few months ago and is quite relevant to my other texture compression posts and is probably more a prelude to what I am experimenting with at the moment. The base idea is that instead of compressing a texture to a separate format such as JPEG and doing real-time transcoding, what kind of compression could we apply to existing DXT data in order to reduce bandwidth requirements. There has already been some experimentation on the topic with mixed results, but this I something I wanted to attempt for myself if not only as a training exercise.

Actually, I am not just rehashing the results but decided to rework the code more and redo the experiments as some of the initial results I had were somewhat interesting. And I honestly don’t remember all the inner workings of my implementation since this was a few months ago.

### DXT File Data Structure

I will not go into too much details on this since there is plenty of information out there on the topic and will only use DXT1 as a reference here in order not to add the extra complexities due to the alpha channel. DXT textures are compressed in 4×4 pixel blocks and decomposed into two main components, two endpoint colors and a set of 16 selectors of two bits each. The endpoint colors represent the minimum and maximum of the optimal line that minimizes the distance between each of the colors in the block. This line is then assumed to be divided into 4 equidistant values which represent the color corresponding to the four values possible for the two bit selectors.

	color[4] = { start, start + 1/3 ( end - start ), start + 2/3 ( end - start ), end};

The DXT compressor picks the proper selector based on which color from the four values above is the closest to the original color in the DXT block. Since the general structure of both the color values and the selector bits is different, a different compression approach will need to be taken for both of them…

### Compressing Color Values

The compression of the color values is where the meat is. Since I am sticking to losslesss compression, I will avoid JPEG or other similar schemes and stick with something more basic. I made a few assumptions in deciding which approach to take:

1. The two endpoint colors represent the minimum and maximum color along the “minimal error line” of all the colors within a block. Unless the block is a uniform color, there will likely be a significant delta between the minimum and maximum color. To encode the colors, I will group together the minimum and the maximum colors and treat them essentially as two separate images to encode.
2. Unless there is a sharp edge, neighboring colors will likely be close to each other. So it makes sense to encode the deltas between neighbors. The use of a predication algorithm will likely also reduce the entropy of the deltas.
3. It is likely best to work on a channel per channel basis, which could potentially allow the conversion to a more efficient color space. Will do my initial testing using a YCrCb space as it does a good job of maximizing energy in the Y channel.
4. The entropy coding part is a little unclear, mainly depends on what type of distribution the color deltas have. Of course, I myself already know the answer to this part of the puzzle but a Huffman coder would yield good general results, unless the statistics of the data point to a coding scheme that is better suited to that distribution.

For the prediction scheme, I decided to stick with something quite simple. Since the scanning of pixels is done left-right/top-down, unless you are at a top of left edge, the pixel to the left and above you will always be available. Using this knowledge, I can make a prediction taking advantage those existing pixels. I initially take a look at top, top-left and left pixel and determine the general direction of the color gradient. With the gradient in mind, we can determine which of the three pixels is most likely similar to the current pixel and use this value. With our predicted value, we can determine the delta for the specific pixel (and obviously repeat the pattern for all the pixels in the image).

This brings up the question of which entropy encoder to use to complete the process. Before making a decision, I decided to run the existing algorithm on some representative pixels and print out a graph of the statistics per color component.

http://www.sebbylive.com/wp-content/uploads/2011/07/dxtstat1.jpg

The graphs are actually quite interesting as the show a geometric progression (and I get similar results for most textures). This is a really code case for compression and due to the consistent nature for most test pictures, I decided to employ a [Exponential-Golomb Coder](http://en.wikipedia.org/wiki/Exponential-Golomb_coding) which is optimal in the case of geometric progressions.

I use a variation of this coder which deals with signed values by assuming the bit 0 represents zero and all other values are essentially alternating between positive and negative. I put some code for this in the implementation section below. Also, due to the fact that Golomb coding should be near optimal, no Huffman or other entropy coding of this data should be needed.

### Compressing Selector Bits

Compressing selector bits is a whole different ballgame. Since a color is represented by a pair of two bits and the compression has to be lossless no real compression can be achieved on a per-color basis. The only hope of getting any compression is to group colors together and see if there are any statistical redundancies.

I decided to group blocks of 2×2 pixels together since I assume there would be more correlation there than simply packing them row by row and did a quick statistical analysis of the coherence of between the generated bytes. Below is a graph which shows the statistical distribution of a representative image:

http://www.sebbylive.com/wp-content/uploads/2011/07/dxtstat2.jpg

From the graph, you can see that there is no distinctive winners. However, there seems to be some combinations which are generally more prevalent. Because of this, I decided a general purpose Huffman should be simple enough and do a good job at extracting any redundancy in the data.

### Implementation

Normally, I would post the complete code implementation for such an algorithm. However, the code is a total mess, a mix of C# and managed C++ code and the user interface does depend on a few external libraries. Instead of dumping this messy hack into the world, it made more sense to discuss the various critical parts of the algorithm and provide relevant snippets as needed.

#### Color Space Conversion

Instead of compressing colors in RGB space, I decided to use a transform which optimizes entropy and allows slightly better compression. There are a variety of options, but I opted for the [YCoCg color space](http://software.intel.com/sites/products/documentation/hpc/ipp/ippi/ippi_ch6/ch6_color_models.html) (or [here](http://wiki.multimedia.cx/index.php?title=YCoCg)) as in addition to offering good perceptual and entropy compaction, it offers a straightforward integer implementation which allows for fast conversion.

Conversion From RGB to YCoCg:

	Y = CLAMP_BYTE(( R + (G << 1) + B ) >> 2 );
	Co = CLAMP_BYTE((( R - B ) >> 0) + 128);
	Cg = CLAMP_BYTE((( G - ((R + B) >> 1)) >> 0) + 128);

Conversion From YCoCg to RGB:

	t = Y - (Cg >> 1);
	G = CLAMP_BYTE(Cg + t);
	B = CLAMP_BYTE(t - (Co >> 1));
	R = CLAMP_BYTE(B + Co);

#### Color Prediction

As I have discussed earlier, the prediction process was kept simple and is based on the fact that the pixel scanning is done in a left-right/top-bottom order. This means that except for pixels on the top and left border there will always be a decoded pixel available above and to the left of the current pixel. The code below is more complex than needed due to handling border conditions but essentially determines the direction of the gradient in the top, top left and left pixels and assumes the best prediction is in the direction of the least gradient.

	public void ComputeDelta(bool lossyDelta)
	{
	    for (int j = 0; j < 3; j++)
	    {
	        for (int y = 0; y < _height; y++)
	            for (int x = 0; x < _width; x++)
	            {
	                if (x == 0)
	                {
	                    if (y == 0)
	                    {
	                        _deltaData[y, x, j] = 0;
	                    }
	                    else
	                    {
	                        _deltaData[y, x, j] = _colorData[y, x, j] - _colorData[y - 1, x, j];
	                    }
	                }
	                else
	                {
	                    if (y == 0)
	                    {
	                        _deltaData[y, x, j] = _colorData[y, x, j] - _colorData[y, x - 1, j];
	                    }
	                    else
	                    {
	                        int a = _colorData[y, x - 1, j];
	                        int b = _colorData[y - 1, x - 1, j];
	                        int c = _colorData[y - 1, x, j];
							
	                        int dh = Math.Abs(b - c);
	                        int dv = Math.Abs(b - a);
	                        int pred = 0;
	                        if (dv > dh)
	                            pred = a;
	                        else
	                            pred = c;
								
	                        _deltaData[y, x, j] = _colorData[y, x, j] - pred;
	                    }
	                }
	            }
	    }
	}

#### Golomb Encoding and Decoding

The Exponential-Golomb Coding algorithm come in quite handy in order to encode the With a little understand of the algorithm, it should be fairly easy to interpret the code below. Keep in mind that my implementation takes into account signed numbers by alternating them in the Golomb representation:

	public void ExpGolombEncode(BitStream stream)
	{
	    for (int j = 0; j < 3; j++)
	    {
	        for (int y = 0; y < _height; y++)
	            for (int x = 0; x < _width; x++)
	            {
	                UInt16 val = 0;
	                if (_deltaData[y, x, j] < 0)
	                    val = (UInt16)(-1 - 2 * _deltaData[y, x, j]);
	                else
	                    val = (UInt16)(2 * _deltaData[y, x, j]);
	                val++;
					
	                int n = 0;
	                UInt16 c = val;
	                while (c != 0)
	                {
	                   if (n != 0) stream.Write(false);
	                   c >>= 1; n++;
	                }
					
	                n--;
	                stream.Write(true);
	                while (n != 0)
	                {
	                   n--;
	                   stream.Write((val & (1 << n)) != 0);
	                }
	            }
	    }
	}
	
	public void ExpGolombDecode(BitStream stream)
	{
	    for (int j = 0; j < 3; j++)
	    {
	       for (int y = 0; y < _height; y++)
	           for (int x = 0; x < _width; x++)
	           {
	                int n = 0;
	                bool curBit = true;
	                stream.Read(out curBit);
	                while (!curBit)
	                {
	                    n++;
	                    stream.Read(out curBit);
	                }
					
	                UInt16 val = 1;
	                curBit = false;
	                while (n > 0)
	                {
	                    stream.Read(out curBit);
	                    val <<= 1;
	                    if (curBit) val |= 1;
	                    n--;
	                }
	                val--;
					
	                int oldVal = _deltaData[y, x, j];
	                if ((val & 0x1) != 0)
	                    _deltaData[y, x, j] = -((val + 1) >> 1);
	                else
	                    _deltaData[y, x, j] = (val >> 1);
	            }
	    }
	}

#### Experimental Results and Conclusions

To test the algorithm, I created a little GUI application which displays the before and after of the compression (and a few lossy modes I was playing with) as well as some of the statistical graphs shown earlier. I used a variety of game textures to test out the algorithm.

In general, the algorithm preformed fairly consistently giving compression rates in the 40% range. It would likely perform poorly in noisy textures and slightly better in textures with a fair number of solid colors. I’ve included a screen grab below of a few examples to illustrate some of the compression results.

http://www.sebbylive.com/wp-content/uploads/2011/07/dxt_lossless1.png
The image on the left is the original and the compressed image is on the right, and of course the look exactly the same. Below are some stats about the compression. As you can see, the lossless compression seems to achieve roughly 40% compression.

### Experiments with Lossy Compression

A little extra section to talk about lossy compression. One additional experiment I did do as part of this project was to add a simple lossy scheme to the compression algorithm above. The idea was simple, if the delta for a color channel was at the boundary of one of the Golomb buckets, skew the delta by one in order to bring it back down to the previous bucket and therefore save a few bits.

In general, this added about another 10% to the overall compression but opened up it’s own cans of worm…

Because even small deltas were being shrunk, this lead to blockiness as small color variations would get brought down to zero. Also, since lossy corrections were being pushed out to the neighboring pixels to avoid drift, the compressor would eventually catch up once there was enough accumulated error to put the bit count to the next Golomb bucket, which in turn lead to a banding effect.

http://www.sebbylive.com/wp-content/uploads/2011/07/dxt_lossy1.png
In this image, the top left image is the original, the top right is the lossless compressed image, the bottom left is the lossy encoder and the bottom right is a DCT compression based experiment I also did. You can see the blockiness and banding in the lossy version of the compression.