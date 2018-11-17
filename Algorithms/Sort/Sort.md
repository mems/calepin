- [The fxt demos: sorting and searching](http://www.jjj.de/fxt/demo/sort/index.html)
- [The Improved Sorting Algorithm Demo](http://cglab.ca/~morin/misc/sortalg/)
- [ValveBlog: AS3 sorting algorithm faster than native sorting](http://wayback.archive.org/web/20090617210241/http://www.valveblog.com/2009/06/as3-sorting-algorithm-faster-than-native-sorting.html)
 
	package
	{
		import flash.display.Sprite;
		import flash.utils.getTimer;
		
		/**
		* Vector sorting methods test
		*
		* @author Eugene Zatepyakin
		* @see http://blog.inspirit.ru/?p=271
		*/
		public class Main extends Sprite
		{
			
			public function Main()
			{
				test();
			}
			
			private function test():void
			{
				var t:int = 100000;
				var arr:Vector.<Number> = new Vector.<Number>(t, true);
				var arr2:Array = [];
				var arr1:Vector.<Number>;
				
				for (var i:int = 0; i < t; i++)
				{
				var nn:Number = 1000 - Math.random() * 2000;
				arr[i] = nn;
				arr2[i] = nn; // this one is for built in array.sort
				}
				
				var tt:int;
				
				// Quick Sort + Insertion Sort
				// I guess this one could be faster
				// if we only could merge two functions in to one
				arr1 = arr.concat();
				tt = getTimer();
				
				qsort(arr1, 0, int(t - 1));
				InsertionSort(arr1, 0, int(t - 1));
				
				trace('qsort+insert:', getTimer() - tt);
				//checkSort(arr1);
				
				// 3 Way Quick Sort
				arr1 = arr.concat();
				tt = getTimer();
				
				qsort3Way(arr1, 0, int(t - 1));
				
				trace('3way qsort:', getTimer() - tt);
				//checkSort(arr1);
				
				// Non Recursive Quick Sort
				arr1 = arr.concat();
				tt = getTimer();
				
				nonRecursiveQuickSort(arr1, 0, int(t - 1));
				
				trace('non recursive qsort:', getTimer() - tt);
				//checkSort(arr1);
				
				// Optimized Non recursive qsort
				arr1 = arr.concat();
				tt = getTimer();
				
				OptNonRecursiveQuickSort(arr1, 0, (t - 1));
				
				trace('opt non recursive qsort:', getTimer() - tt);
				//checkSort(arr1);
				
				// Non Recursive qsort 2
				arr1 = arr.concat();
				tt = getTimer();
				
				nonRecursiveQsort2(arr1, t);
				
				trace('non recursive qsort2:', getTimer() - tt);
				//checkSort(arr1);
				
				// Flash Sort
				arr1 = arr.concat();
				tt = getTimer();
				
				flashSort(arr1, t);
				
				res += '\nFlash Sort\t\t\t\t\t' + (getTimer() - tt).toString();
				//checkSort(arr1);
				
				// Built in Array sort
				tt = getTimer();
				arr2.sort(Array.NUMERIC);
				
				trace('array.sort:', getTimer() - tt);
			}
			
			public function InsertionSort(arr:Vector.<Number>, n:int):void
			{
				var i:int, j:int, v:Number;
				for(j = 1; j < n; ++j)
				{
					v = arr[j];
					i = int(j - 1);
					while(i >= 0 && arr[i] > v)
						arr[int(i+1)] = arr[ int(i--) ];
					arr[int(i+1)] = v;
				}
			}
			
			public function qsort(arr:Vector.<Number>, l:int, r:int):void
			{
				var i:int, j:int, k:int, vi:int, v:Number;
				
				if ((r - l) > 10) 
				{
				i = int(r + l) >> 1;
				if (arr[l] > arr[i]) 
				{
				vi = arr[l];
				arr[l] = arr[i];
				arr[i] = vi;
				}
				
				if (arr[l] > arr[r]) 
				{
				vi = arr[l];
				arr[l] = arr[r];
				arr[r] = vi;
				}
				
				if (arr[l] > arr[r]) 
				{
				vi = arr[i];
				arr[i] = arr[r];
				arr[r] = vi;
				}
				
				j = int(r - 1);
				
				vi = arr[i];
				arr[i] = arr[j];
				arr[j] = vi;
				
				i = l;
				v = arr[j];
				
				while (true) 
				{
				while (arr[ int(++i) ] < v);
				while (arr[ int(--j) ] > v);
				
				if (j < i) break;
				
				vi = arr[i];
				arr[i] = arr[j];
				arr[j] = vi;
				}
				
				vi = arr[i];
				arr[i] = arr[ (k = int(r - 1)) ];
				arr[k] = vi;
			
				qsort(arr, l, j);
				qsort(arr, int(++i), r);
				}
			}
	
			private function qsort3Way(arr:Vector.<Number>, l:int, r:int):void
			{
				if((r - l) <= 10) return;
				
				var i:int = int(l - 1), j:int = r, p:int = int(l - 1), q:int = r, vi:Number;
				
				//if (r <= l) return;
				
				var v:Number = arr[r];
				
				while (true)
				{
				while (arr[ int(++i) ] < v);
				while (v < arr[ int(--j) ]) {
				if (j == l) break;
				}
				
				if (i >= j) break;
				
				vi = arr[i];
				arr[i] = arr[j];
				arr[j] = vi;
				
				if (arr[i] == v) 
				{
				vi = arr[ int(++p) ];
				arr[p] = arr[i];
				arr[i] = vi;
				}
				if (v == arr[j]) 
				{
				vi = arr[j];
				arr[j] = arr[ int(--q) ];
				arr[q] = vi;
				}
				}
				
				vi = arr[i];
				arr[i] = arr[r];
				arr[r] = vi;
				
				j = int(i - 1);
				i = int(i + 1);
				
				for (var k:int = l; k < p; ++k, --j) 
				{
				vi = arr[k];
				arr[k] = arr[j];
				arr[j] = vi;
				}
				for (k = (r - 1); k > q; --k, ++i) 
				{
				vi = arr[i];
				arr[i] = arr[k];
				arr[k] = vi;
				}
				
				qsort3Way(arr, l, j);
				qsort3Way(arr, i, r);
			}
			
			public function nonRecursiveQuickSort(arr:Vector.<Number>, min:int, max:int):void
			{
				var Stack:Vector.<int> = new Vector.<int>(128, true); // Stack for array bounds
				var top:int = -1;
				var n:int = int(max + 1);
				var pivot:Number, temp:Number;
				var pivotindex:int, l:int, r:int, i:int, j:int;
				
				Stack[ int(++top) ] = min;	// Initialize stack
				Stack[ int(++top) ] = max;
				
				while (top > 0) // While there are unprocessed subarrays 
				{	
				// Pop Stack
				j = Stack[ int(top--) ];
				i = Stack[ int(top--) ];
				
				// Findpivot
				pivotindex = int(i+j) >> 1;
				pivot = arr[pivotindex];
				
				// Stick pivot at end
				arr[pivotindex] = arr[j];
				arr[j] = pivot;
				
				// Partition
				l = (i - 1);
				r = j;
				do 
				{
				while (arr[ int(++l) ] < pivot);
				while ((r!=0) && (arr[ int(--r) ] > pivot));
				temp = arr[l];
				arr[l] = arr[r];
				arr[r] = temp;
				} while (l < r);
				
				// Undo final swap
				temp = arr[l];
				arr[l] = arr[r];
				arr[r] = temp;
				
				// Put pivot value in place
				temp = arr[l];
				arr[l] = arr[j];
				arr[j] = temp;
				
				// Put new subarrays onto Stack if they are small
				if ((l-i) > 10) // Left partition / 10 could be adjusted from 0 - …
				{
				Stack[ int(++top) ] = i;
				Stack[ int(++top) ] = (l-1);
				}
				
				if ((j-l) > 10) // Right partition / 10 could be adjusted from 0 - …
				{
						Stack[ int(++top) ] = (l+1);
						Stack[ int(++top) ] = j;
					}
				}
				
				for(j = 1; j < n; ++j)
				{
					temp = arr[j];
					i = int(j - 1);
					while(i >= 0 && arr[i] > temp)
						arr[int(i+1)] = arr[ int(i--) ];
					arr[int(i+1)] = temp;
				}
			}
	
			public function OptNonRecursiveQuickSort(c:Vector.<Number>, min:int, max:int):void
			{
				var i:int, j:int, left:int = min, right:int = max, stack_pointer:int = -1;
				var median:int;
				var stack:Vector.<int> = new Vector.<int>(128, true);
				var swap:Number, temp:Number;
				
				while(true){
					if(right - left <= 10) // use insertion sort
					{
						for(j = int(left+1); j <= right; ++j)
						{
							swap = c[j];
							i = int(j - 1);
							while(i >= left && c[i] > swap)
								c[int(i+1)] = c[ int(i--) ];
							c[int(i+1)] = swap;
						}
						
						if(stack_pointer == -1) break;
						
						right = stack[ int(stack_pointer--) ];
						left = stack[ int(stack_pointer--) ];
					} else {
						median = int(left + right) >> 1;
						i = (left + 1);
						j = right;
						
						swap = c[median]; c[median] = c[i]; c[i] = swap;
						
						if(c[left] > c[right])
						{
							swap = c[left]; c[left] = c[right]; c[right] = swap;
						}
						if(c[i] > c[right])
						{
							swap = c[i]; c[i] = c[right]; c[right] = swap;
						}
						if(c[left] > c[i])
						{
							swap = c[left]; c[left] = c[i]; c[i] = swap;
						}
						
						temp = c[i];
						
						while(true){
							//do i++; while(c[i] < temp);
							//do j--; while(c[j] > temp);
							while(c[ int(++i) ] < temp);
							while(c[ int(--j) ] > temp);
							
							if(j < i) break;
							
							swap = c[i]; c[i] = c[j]; c[j] = swap;
						}
						
						c[int(left + 1)] = c[j];
						c[j] = temp;
						if((right-i+1) >= (j-left))
						{
							stack[ int(++stack_pointer) ] = i;
							stack[ int(++stack_pointer) ] = right;
							right = int(--j);
						} else {
							stack[ int(++stack_pointer) ] = left;
							stack[ int(++stack_pointer) ] = int(--j);
							left = i;
						}
					}
				}
			}
			
			public function nonRecursiveQsort2(arr:Vector.<Number>, els:int):void
			{
				var piv:Number, i:int = 0, j:int, L:int, R:int;
				var beg:Vector.<int> = new Vector.<int>(128, true);
				var end:Vector.<int> = new Vector.<int>(128, true);
				
				beg[0] = 0; end[0] = els;
				while (i >= 0)
				{
				L = beg[i]; R = end[i] - 1;
				if (L < R)
				{
				piv = arr[L];
				while (L < R)
				{
				while (arr[R] >= piv && L<R) --R; if (L<R) arr[ int(L++) ] = arr[R];
				while (arr[L] <= piv && L<R) ++L; if (L<R) arr[ int(R--) ] = arr[L];
				}
				arr[L] = piv; beg[ (j = int(i+1)) ] = (L+1); end[j] = end[i]; end[ int(i++) ] = L;
				}
				else {
						--i;
						}
				}
			}
			
			public function flashSort(a:Vector.<Number>, n:int):void
			{
				var i:int = 0, j:int = 0, k:int = 0, t:int;
				var m:int = int(n * .125);
				var l:Vector.<int> = new Vector.<int>(m);
				var anmin:Number = a[0];
				var nmax:int	= 0;
				var nmove:int = 0;
	
				for (i = 1; i < n; ++i)
				{
				if (a[i] < anmin) anmin = a[i];
				if (a[i] > a[nmax]) nmax = i;
				}
	
				if (anmin == a[nmax]) return;
	
				var c1:Number = (m - 1) / (a[nmax] - anmin);
	
				for (i = 0; i < n; ++i)
				{
				k = int(c1*(a[i] - anmin));
				++l[k];
				}
	
						for (k = 1; k < m; ++k)
				{
				l[k] += l[int(k-1)];
				}
	
				var hold:Number = a[nmax];
				a[nmax] = a[0];
				a[0] = hold;
	
				var flash:Number;
				j = 0;
				k = int(m - 1);
				i = int(n - 1);
	
				while (nmove < i)
				{
				while (j > (l[k]-1))
				{
				k = int(c1 * (a[ int(++j) ] - anmin));
				}
	
				flash = a[j];
	
				while (!(j == l[k]))
				{
				k = int(c1 * (flash - anmin));
				hold = a[ (t = int(l[k]-1)) ];
				a[ t ] = flash;
				flash = hold;
				--l[k];
				++nmove;
				}
				}
	
				for(j = 1; j < n; ++j)
				{
					hold = a[j];
					i = int(j - 1);
					while(i >= 0 && a[i] > hold)
						a[int(i+1)] = a[ int(i--) ];
					a[int(i+1)] = hold;
				}
			}
	
			public function checkSort(arr:Vector.<Number>):void
			{
				var n:int = arr.length;
				for (var i:int = 1; i < n; ++i)
				{
					if (arr[int(i - 1)] > arr[i])
					{
						trace("bad sort");
						return;
					}
				}
				trace('sort ok');
			}
	
		}
	}

	package
	{
		import flash.display.Sprite;
		import flash.events.Event;
		import flash.utils.getTimer;
		
		public class Sorting extends Sprite {
			public function Sorting() {
				addEventListener(Event.ENTER_FRAME, loop);
			}
			private function loop(e:Event):void {
				var data:Vector.<Number> = new Vector.<Number>();
				for(var i:int = 0; i<10000; i++){
					data.push(Math.random()*10000);
				}
				var data2:Vector.<Number> = data.concat();
				var t:Number = getTimer();
				data.sort(sf);
				trace("Native sort", (getTimer()-t));
				t = getTimer();
				data.sort(sf);
				trace("Native sort on ordered elements", (getTimer()-t));
				t = getTimer();
				shellSort(data2);
				trace("AS3 Shell sort", (getTimer()-t));
				t = getTimer();
				shellSort(data2);
				trace("AS3 Shell sort on ordered elements", (getTimer()-t));
			}
			final private function sf(a:Number, b:Number):int {
				return (a==b ? 0 : (a < b) ? -1 : 1);
			}
			final private function shellSort(data:Vector.<Number>):void {
				var n:int = data.length;
				var inc:int = int(n/2);
				while(inc) {
				for(var i:int=inc; i<n; i++) {
				var temp:Number = data[i], j:int = i;
				while(j >= inc && data[int(j - inc)] > temp) {
				data[j] = data[int(j - inc)];
				j = int(j - inc);
				}
				data[j] = temp
				}
				inc = int(inc / 2.2);
				}
			}
		}
	}
