# Binary Search 二分搜尋法
:fire:注意使用者方法之前，必須是已經排序過的陣列。

在搜尋時，會先取陣列的中間值進行比較，如果目標值比中間值小，就往左半邊的陣列繼續去搜尋，如果目標值比中間值大，就往右邊找，並且依據上述的原則，重複執行，直到找到為止。

```js
function BinearSearch(arr, value) {
	let left = 0;
	let right = arr.length - 1;

	while (left <= right) {
		let mid = Math.floor((left + right) / 2)

		if (arr[mid] > value) {
			right = mid - 1;
		} else if (arr[mid] < value) {
			left = mid + 1;
		} else {
			return mid;
		}
	}

	return -1;
}
```