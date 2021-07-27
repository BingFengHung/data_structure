# Merge Sort 合併排序法
合併排序法，簡單來說就是將元素先拆開，進行比較之後，在合併。

- 拆開
1. 將陣列拆開為兩個陣列
2. 再將拆開的陣列繼續拆開直到每個小陣列，僅有一個元素

- 合併
1. 將兩個只剩下一個元素的陣列合併
2. 將前一步排序好的陣列，再與其他合併好的陣列合併，最終成為一個大陣列。

```js
function mergeSort(arr) {
	if (arr.length <= 1) {
	   return arr;
    }
	else {
		let leftArr = arr.slice(0, arr.length / 2)
		let rightArr = arr.slice(arr.length / 2 , arr.length)
		
		let mergeLeft = mergeSort(leftArr)
		let mergeRight = mergeSort(rightArr)

		let tempArr = []

		let i = 0;
		let j = 0;

		while(mergeLeft.length > i && mergeRight.length > j) {
			if (mergeLeft[i] < mergeRight[j]) {
				tempArr.push(mergeLeft[i])
				i++;
			} else if (mergeLeft[i] > mergeRight[j]){
				tempArr.push(mergeRight[j])
				j++;
			} 
		} 
		
		while(mergeLeft.length > i) { 
			tempArr.push(mergeLeft[i]);
			i++;
		} 
		
		while(mergeRight.length > j) { 
			tempArr.push(mergeRight[j]);
			j++; 
		}

		return tempArr;
	}
}

```