# Bucket Sort 桶子排序法
準備幾個桶子，將要排序的`資料分類`置至指定的桶子中，再依序將桶子裡面的東西取出。

1. 將資料分類
2. 丟進指定的桶子
3. 依序將桶子裡的東西取出

```js
function bucketSort(arr) {
    max_score = 100
    // 先產生一堆桶子
    var bucket = new Array(101).fill(0)

    // 在對應的桶子上加一
    for(let i = 0 ; i < arr.length; i++) {
        bucket[arr[i]] = bucket[arr[i]] + 1
    }
    
    let index = 0;
    // 從桶子中取出資料
    for(let i = 0; i < bucket.length; i++) {
        if (bucket[i] !== 0) {
            for (let j = 0; j < bucket[i]; j++) {
                // 將資料寫還原本的陣列中
                arr[index] = i;
            
                index++;
            }
        }
    }

    return arr;
}
```