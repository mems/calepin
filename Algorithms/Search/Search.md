- [Improving the performance of full-text search | Dropbox Tech Blog](https://blogs.dropbox.com/tech/2016/09/improving-the-performance-of-full-text-search/)
- [An interactive explanation of quadtrees.](http://jimkang.com/quadtreevis/)
- [Regular Expression Matching with a Trigram Index](https://swtch.com/~rsc/regexp/regexp4.html) - Search with regular expression in large document set https://github.com/google/codesearch
- [Debian Code Search](https://codesearch.debian.net/) - https://codesearch.debian.net/research/bsc-thesis.pdf
- [etsy/hound: Lightning fast code searching made easy](https://github.com/etsy/hound)

- Soundex(phonetics): semi-tolerant to misspellings and also brings up similar-sounding results http://yomguithereal.github.io/talisman/phonetics/#fuzzy-soundex
- Damerau-Levenshtein is used to sort the results by closeness http://yomguithereal.github.io/talisman/metrics/distance#damerau-levenshtein

See also [Tree search](Tree traversal#tree-search)
 
	function get_nearest_keyframe(second:Number, keytimes)
	{
		var index1 = 0;
		var index2 = 0;
		// Iterate through array to find keyframes before and after scrubber second
		for(var i = 0; i != keytimes.length; i++)
		{
			if(keytimes[i] < second)
			{
				index1 = i;
			}
			else
			{
				index2 = i;
				break;
			}
		}
		// Calculate nearest keyframe
		if(second - keytimes[index1] < keytimes[index2] - second)
		{
			return index1;
		}
		else
		{
			return index2;
		}
	}
