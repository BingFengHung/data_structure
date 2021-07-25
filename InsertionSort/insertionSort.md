# Insertion Sort 插入排序法
插入排序法，會將資料分為`已排序`資料與`未排序`資料。

插入時，會`由右而左`比較，當碰到比當前欲插入的值要小時，往左移動插入；若值比較大，則往右插入。

```js
function insertionSort(arr) {
	let temp = undefined;
	// 陣列第一個索引值當作已排序，所以從 1 開始
	for (let i = 1; i < arr.length; i++) {
		for (let j = i; j > 0; j--) {
			if (arr[j] < arr[j - 1]) {
				swap(arr, j, j - 1);
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