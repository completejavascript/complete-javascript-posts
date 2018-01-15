Từ xưa đến nay, sắp xếp giữ một vai trò vô cùng quan trọng. Nhiều ứng dụng (từ điển, danh bạ, quản lý tài khoản,…) thường có chức năng sắp xếp theo thứ tự từ điển (a-z). Việc này giúp cho người quản lý và người dùng dễ dàng tìm kiếm nội dung hơn. Do đó, trong bài viết này, tôi sẽ cùng với các bạn tìm hiểu về vấn đề [Array](https://completejavascript.com/javascript-array-co-ban/) Sorting trong JavaScript.

Về sắp xếp nói chung, chúng ta có rất nhiều thuật toán với độ phức tạp khác nhau, có thể kể đến là: selection sort, insertion sort, binary insertion sort, interchange sort, bubble sort, shaker sort, quick sort, merge sort, heap sort,…

(Xem thêm hai bài tổng hợp về thuật toán sắp xếp trong C/C++: [phần 1](http://thuattoan.phamvanlam.com/tong-hop-mot-so-thuat-toan-co-ban-ve-sap-xep-phan-1/), [phần 2](http://thuattoan.phamvanlam.com/tong-hop-mot-so-thuat-toan-co-ban-ve-sap-xep-phan-2/))

Tuy nhiên, bạn không cần thiết phải implement lại những thuật toán sắp xếp này. Vì JavaScript hỗ trợ sẵn cho chúng ta một [function](https://completejavascript.com/tim-hieu-function-javascript/) để sắp xếp.

## Cú pháp:

```js
arr.sort()
arr.sort(compareFunction)
```

### Tham số

**compareFunction**: dùng để xác định thứ tự sắp xếp. Nếu bạn bỏ qua tham số này thì mặc định JavaScript sẽ sắp xếp theo thứ tự tăng dần trong bảng mã Unicode (hay đơn giản thì cứ gọi là thứ tự tăng dần bảng chữ cái).

### Giá trị trả về

Mảng đã được sắp xếp (và mảng ban đầu có bị thay đổi).

```js
var a = ['c', 'g', 'w', 'a'];
var b = a.sort();
console.log(a); // => ["a", "c", "g", "w"]
console.log(b); // => ["a", "c", "g", "w"]
```

## Tìm hiểu compareFunction

Hàm *compareFunction* dùng để xác định thứ tự sắp xếp. Nếu a và b là hai phần tử dùng để so sánh thì:
  * Nếu compareFunction(a, b) trả về < 0 thì a sẽ đứng trước b.
  * Nếu compareFunction(a, b) trả về > 0 thì a sẽ đứng sau b.
  * Nếu compareFunction(a, b) trả về = 0 thì không sắp xếp (giữ nguyên thứ tự).
 
## Array sorting với numbers

JavaScript hỗ trợ sắp xếp nhiều kiểu dữ liệu. Tuy nhiên, phổ biến nhất vẫn là [numbers](https://completejavascript.com/values-types-va-operators-trong-javascript-phan-1/). Và như tôi đã nói ở trên, mặc định hàm sort sẽ so sánh theo kiểu [string](https://completejavascript.com/values-types-va-operators-trong-javascript-phan-2/). Do đó, kết quả sẽ như thế này:

```js
var a = [9, 100, 45, 33];
console.log(a.sort());
// => [100, 33, 45, 9]
```

Bạn không nhìn lầm đâu. Kết quả trên là hoàn toàn chính xác. Vì khi so sánh theo kiểu string thì ‘1’ < ‘3’ < ‘4’ < ‘9’. Vì vậy, để sắp xếp chúng theo kiểu numbers thì bạn cần phải sử dụng hàm compareFunction.

### Sử dụng hàm compareNumbers sắp xếp numbers theo thứ tự tăng dần

```js
function compareNumbers(a, b) {
  return a - b;
}
var a = [9, 100, 45, 33];
console.log(a.sort(compareNumbers));
// => [9, 33, 45, 100]
```

Theo đúng mô tả của hàm compareFunction, khi a < b => a – b < 0 => a sẽ đứng trước b. Nghĩa là số bé hơn sẽ đứng trước. Áp dụng quy tắc này, ta được mảng các số sắp xếp theo thứ tự tăng dần.

Ngoài cách viết hàm riêng như trên, bạn có thể áp dụng [JavaScript closures](https://completejavascript.com/tim-hieu-javascript-closures/):

```js
var a = [9, 100, 45, 33];
console.log(a.sort(function(a, b){
	return a - b;
}));
// => [9, 33, 45, 100]
```

### Sắp xếp numbers theo thứ tự giảm dần

Để sắp xếp mảng numbers theo thứ tự giảm dần thì bạn chỉ cần thay đổi nội dung hàm compareNumbers. Thay vì return a – b thì bây giờ tôi sẽ return b – a.

```js
var a = [9, 100, 45, 33];
console.log(a.sort(function(a, b){
	return b - a;
}));
// => [100, 45, 33, 9]
```

Bây giờ, khi a < b => b – a > 0 => a sẽ đứng sau b. Nghĩa là số nhỏ hơn sẽ đứng sau. Do đó, kết quả thu được là dãy số giảm dần như trên.

Trên đây là cách sử dụng hàm sort (mặc định) của [JavaScript](https://completejavascript.com/category/javascript-co-ban/) để sắp xếp mảng. Tuy nhiên, nếu như bạn không muốn sử dụng hàm mặc định này thì bạn vẫn có thể tự implement sử dụng một số thuật toán sắp xếp cơ bản.

## Array sorting trong JavaScript sử dụng thuật toán

Nếu bạn từng học ít nhất một ngôn ngữ lập trình như C/C++, Java,… thì tôi dám chắc là bạn đã implement thuật toán sắp xếp rồi.

Một số thuật toán cơ bản là:

  * Thuật toán sắp xếp chọn trực tiếp – Selection Sort
  * Sắp xếp chèn trực tiếp – Insertion Sort
  * Sắp xếp chèn trực tiếp dựa trên tìm kiếm nhị phân – Binary Insertion Sort
  * Thuật toán sắp xếp đổi chỗ trực tiếp – Interchange Sort
  * Sắp xếp nổi bọt – Bubble Sort
  * Thuật toán Shaker Sort
  * Sắp xếp nhanh – Quick Sort
  * Sắp xếp trộn – Merge Sort
  * Sắp xếp vun đống – Heap Sort
 
### Array sorting với sắp xếp chọn trực tiếp – [Selection Sort](https://en.wikipedia.org/wiki/Selection_sort)

```js
function selectionSort(array){
 for(let i = 0; i < array.length - 1; i++){
   let idmin = i;
   for(let j = i + 1; j < array.length; j++){
     if(array[j] < array[idmin]) idmin = j;
   }

   // swap
   let t = array[i];
   array[i] = array[idmin];
   array[idmin] = t; 
 }
}
```

### Sắp xếp chèn trực tiếp – Insertion Sort

```js
function insertionSort(array){
  let pos, x;
  for(let i = 1; i < array.length; i++){
    pos = i - 1;
    x = array[i];
    while(pos >= 0 && array[pos] > x){
      array[pos + 1] = array[pos];
      pos--; 
    }
    array[pos + 1] = x;
  }
}
```

### Sắp xếp chèn trực tiếp dựa trên tìm kiếm nhị phân – Binary Insertion Sort

```js
function binaryInsertionSort(array){
 let l, r, m, x;
 for(let i = 1; i < array.length; i++){
   l = 0;
   r = i - 1;
   x = array[i];
 
   while(l <= r){
     m = Math.floor((l + r) / 2);
     if(array[m] > x) r = m - 1;
     else l = m + 1;
   }

   for(let j = i; j > l; j--)
     array[j] = array[j - 1];
   array[l] = x;
 }
}
```

### Sắp xếp đổi chỗ trực tiếp – Interchange Sort

```js
function interChangeSort(array){
 for(let i = 0; i < array.length - 1; i++){
   for(let j = i + 1; j < array.length; j++){
     if(array[j] < array[i]){
       let t = array[i];
       array[i] = array[j];
       array[j] = t;
     }
   }
 }
}
```

### Sắp xếp nổi bọt – [Bubble Sort](https://en.wikipedia.org/wiki/Bubble_sort)

```js
function bubbleSort(array){
 for(let i = 0; i < array.length - 1; i++){
   for(let j = array.length - 1; j > i; j--){
     if(array[j] < array[j-1]){
       let t = array[j];
       array[j] = array[j - 1];
       array[j - 1] = t;
     }
   }
 }
}
```

### Thuật toán [Shaker Sort](https://en.wikipedia.org/wiki/Cocktail_shaker_sort)

```js
function shakerSort(array){
    let left, right, k;
 
    left = 0;
    right = array.length - 1;
    k = array.length - 1;
            
    while(left < right)
    {       
        for(let j = right; j > left; j--)
        {
            if(array[j] < array[j - 1])
            { 
                let t = array[j];
                array[j] = array[j - 1];
                array[j - 1] = t;
                k = j;  
            }              
        }
        left = k;
 
        for (let j = left; j < right; j++)
        {  
            if (array[j] > array[j + 1])
            { 
                let t = array[j];
                array[j] = array[j + 1];
                array[j + 1] = t;
                k = j;
            }    
        } 
        right = k;
    }
}
```

### Sắp xếp nhanh – [Quick Sort](https://en.wikipedia.org/wiki/Quicksort)

```js
function quickSort(array, left, right){
	let l = left, r = right;
	let m = Math.floor((l + r) / 2);
	let pivot = array[m];

	while(l <= r){
		while(array[l] < pivot) l++;
		while(array[r] > pivot) r--;
		if(l <= r){
			let t = array[l];
			array[l] = array[r];
			array[r] = t;
			l++;
			r--;
		}
	}

	if(l < right) quickSort(array, l, right);
	if(r > left) quickSort(array, left, r);
}
```

### Sắp xếp trộn – [Merge Sort](https://en.wikipedia.org/wiki/Merge_sort)

```js
function merge(array, left, m, right){
	let l = left, r = m + 1;
	let tmp = [];

	while(l <= m && r <= right){
		if(array[l] < array[r]) tmp.push(array[l++]);
		else tmp.push(array[r++]);
	}

	while(l <= m) tmp.push(array[l++]);
	while(r <= right) tmp.push(array[r++]);

	for(let i = 0; i < tmp.length; i++)
		array[i + left] = tmp[i];
}

function mergeSort(array, left, right){
	if(left < right){
		let m = Math.floor((left + right) / 2);
		mergeSort(array, left, m);
		mergeSort(array, m + 1, right);
		merge(array, left, m, right);
	}
}
```

### Sắp xếp vun đống – [Heap Sort](https://en.wikipedia.org/wiki/Heapsort)

```js
function heapify(array, N, i){
    let left = 2*i + 1, right = 2*i + 2, largest;
		 
    if(left < N && array[left] > array[i]) largest = left;
    else largest = i;
		 
    if(right < N && array[right] > array[largest]) largest = right;
		 
    if(largest != i){
        let t = array[i];
        array[i] = array[largest];
        array[largest] = t;
        heapify(array, N, largest);
    }
}
		     
function buildHeap(array){
    let m = Math.floor(array.length / 2 - 1);
    for(let i = m; i >= 0; i--)
        heapify(array, array.length, i);
}
		     
function heapSort(array){
    buildHeap(array);
		     
    for(let i = array.length - 1; i >= 0; i--)    {
        let t = array[0];
        array[0] = array[i];
        array[i] = t;

        heapify(array, i, 0);
    }
}
```

Trên đây là những vấn đề cơ bản về Array Sorting, cùng với một số thuật toán sắp xếp. Theo tôi, đây là những kiến thức cơ bản và có thể được áp dụng rất nhiều. 

Cuối cùng, xin chào và hẹn gặp lại ở bài viết sau trong series [JavaScript cơ bản](https://completejavascript.com/category/javascript-co-ban/).

Thân ái,

## Tham Khảo

  * [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort?v=control)

**Bản gốc**: [Blog Complete JavaScript](https://completejavascript.com/array-sorting-van-de-muon-thuo/)
