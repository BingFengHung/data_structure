# Quick Sort
先找到一個基準點 (pivot)，然後從陣列的兩邊往中間找，如果右邊找到一個值比基準點小，左標找到一個值比基準點大，就將他們互換。

1. 從陣列中選擇中間作為一個基準點
2. 建立兩個指標，一個指向左邊第一個元素，另一個指向右邊陣列最後一個元素。移動左指標值到找到一個比基準點大的元素；接著，右指標找到一個比基準點小的元素，然後交換。重複上述步驟，直到左指標超過了右指標。這個過程會使得比基準點小的值都排在基準點之前，比基準點大的值會排在基準點右邊。
3. 接著，對於劃分後的小陣列，各自在重複上述步驟。

```js
function quickSort(arr) {
	quick(arr, 0, arr.length - 1);
}

function quick(arr, left, right) {
	let index;

	if (arr.length > 1) {
		index = partition(arr, left, right)

		if (left < index - 1) {
			quick(arr, left, index - 1);
		}

		if (index < right) {
			quick(arr, index, right)
		}
	}
}

function partition(arr, left, right) {
	let pivot = arr[Math.floor((right + left) / 2)],
	    i = left,
			j = right
	
	while(i <= j) {
		// 找 arr[i] 的值比 pivot 大
		while(arr[i] < pivot) {
			i++;
		}

		// 找 arr[j] 的值比 pivot 小
		while(arr[j] > pivot) {
			j--;
		}

		if(i <= j) {
			swap(arr, i, j)
			i++;
			j--;
		}
	}

	return i;
}

function swap(arr, a, b) {
	let temp = arr[a]
	arr[a] = arr[b]
	arr[b] = temp
}
```