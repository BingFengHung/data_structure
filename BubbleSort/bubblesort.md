# Bubble Sort 氣泡排序法
這個排序方法，是透過將較小元素搬到陣列開始，較大的元素則慢慢浮往陣列的最後。


```js

function bubbleSort(arr) {
	for (let i = 0; i < arr.length; i++) {
		for (let j = i + 1; j < arr.length; j++) {
			if (arr[i] > arr[j]) {
				swap(arr, i, j)
			}
		}
	}
}

function swap(arr, a, b) {
	let temp = arr[a];
	arr[a] = arr[b];
	arr[b] = temp;
}
```