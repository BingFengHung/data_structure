# Linear Search 線性搜尋法
線性搜尋法就是從第一個元素開始，往後找找到目標元素為止。

如果有找到回傳陣列索引值，如果沒有找到回傳 -1

```js
function LinearSearch(arr, value) {
	for (let i = 0; i < arr.length; i++) {
		if (arr[i] === value) {
			return i;
		} 
	}

	return -1;
}
```