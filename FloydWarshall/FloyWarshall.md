# FloyWarshall 最短路徑
圖形除了廣度與深度演算法基本的演算法之外，還有須多其他求得最短路徑的演算法。

作法為
1. 先建立圖形節點的二維陣列表，表明點到點之間的距離
2. 可能途中或經過多次中轉，與初始的路徑比較，如果能讓兩點之間的路徑變短就更新。
3. 就這樣重複更新矩陣找到最短距離

```js
// FolydWarshall 求圖形的最短路徑
let n = 4
//let e = Array(10).fill(Array(10).fill(0, 0, 10));
let e = []

for(let i = 0; i < 10; i++) {
    e.push([]);
    for (let j = 0; j < 10; j++) {
        e[i].push(0)
    }
}

let infinity = Number.MAX_VALUE

for(let i = 1; i < n + 1; i++) {
    for(let j = 1; j < n + 1; j++) {
        if (i === j) {
            e[i][j] = 0
        } else {
            e[i][j] = infinity;
        }
    }
}

// set default data
e[1][2] = 2;
e[1][3] = 6;
e[1][4] = 4;
e[2][3] = 3;
e[3][1] = 7;
e[3][4] = 1;
e[4][1] = 5;
e[4][3] = 12;



// Floyd-Warshall
for(let k = 1; k < n + 1; k++) {
    for (let i = 1; i < n + 1; i++) {
        for (let j = 1; j < n + 1; j++) {
            let val = e[i][k] + e[k][j]

            if (e[i][j] > val) {
                e[i][j] = val
            }
        }
    }
}

for (let i = 1; i < n + 1; i++) {
    let str = ''
    for(let j = 1; j < n+1;j++) {
        str += e[i][j] + " "
    }
    console.log(str)
}
```