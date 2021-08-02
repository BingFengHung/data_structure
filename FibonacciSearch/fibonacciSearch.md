# Fibonacci Search 費式搜尋

一個已排序的資料，使用費式數列的概念取找到目標值

是先求出費式數列，費式數列裡面的值會拿來當作查找資料的索引值。

1. 先求出費式數列，費式數列裡面的值會用來當作查找資料的索引值。
2. 用待查詢的陣列的陣列長度，來和廢式數列裡面的值做比較，在費式數列中找出小於或等於陣列長度的值，並取其索引值。
3. 設定要如何從查找資料中找尋，從待查詢陣列的索引最大值減去剛剛在費式數列中索引值所對應的值。
4. 設定從費式數列的第幾個索引開始找要給查詢資料找樹姿的索引值。

5. 如果查找資料在索引值大於指定的搜尋值，則第一個搜尋未舅舅式該所引的位置，如果小於指定搜尋值，澤第一個搜尋位置必須加上剛剛第三步的值。

```js
function createFibinacciSerial(arrLength) {
    let arr = [0, 1];

    for (let i = 2; i < arrLength; i++) {
        arr[i] = arr[i - 1] + arr[i-2]
    }

    return arr;
}

function getY(fib, n) {
    let i = 0;
    while(fib[i] <= n) {
        i += 1
    }

    return i - 1
}

function fibonacciSearch(arr, key) {
    let fibArr = createFibinacciSerial(arr.length)
    // 最大索引值
    let maxIndex = arr.length - 1;


    // 取得費式數列中，比陣列索引值小於或等於最大索引值
    let y = getY(fibArr, arr.length)

    let m = maxIndex - fibArr[y]
    let x = y - 1  // 找到在 arr 搜尋的起始索引值

    let i = x;

    if (fibArr[i] < key) {
        i += m;
    }

    while (fibArr[x] > 0) {
        if (fibArr[i] < key) {
            x--;
            i += fibArr[x]
        }
        else if (fibArr[i] > key) {
            x--;
            i -= fibArr[x]
        } else {
            return i;
        }
    }

    return -1;
}

let number = [10, 22, 30, 55, 56, 58, 60, 70, 100, 110, 130]

console.log(fibonacciSearch(number, 60))
```