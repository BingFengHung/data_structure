# 基數排序法 Radix Sort

利用資料裡面的值得某些特些作為排序的依據。

假設有三個位數的數值，要進行排序

首先從個位數，來進行分配，接著是十位數再來是百位數

```js
let data = [89, 34, 23, 78, 67, 100, 66, 29, 79, 55, 78, 88, 92, 96, 96, 23]

function radixSort(arr) {
    // 找尋陣列中的最大數
    let max = Math.max(...arr)


    for(let i = 0; i < max; i++) {
        // 建立 buckets\
         let buckets = Array.from({length:10}, () => [])

        for (let j = 0; j < arr.length; j++) {
            buckets[getPosition(arr[j], i)].push(arr[j])
        }

        arr = [].concat(...buckets)
    }

    return arr;
 }

 function getPosition(num, place) {
     return Math.floor(num / Math.pow(10, place)) % 10;
 }

 radixSort(data)
```