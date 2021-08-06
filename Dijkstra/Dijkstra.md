# Dijkstra 求最短路徑
主要內容是指定一個點到其餘各個頂點的最短路徑，也稱作「單源最短路徑」。

```js
let e = Array(10).fill(0).map(i => Array(10).fill(0))
let infinity = 9999999
let keyPoint = 1

let n = 6;
let m = 9;

for (let i = 1; i < n+1; i++) {
    for (let j = 1; j < n + 1; j++) {
        if (i === j) {
            e[i][j] = 0
        } else {
            e[i][j] = infinity;
        }
    }
}

e[1][2] = 1
e[1][3] = 12
e[2][3] = 9
e[2][4] = 3
e[3][5] = 5
e[4][3] = 4
e[4][5] = 13
e[4][6] = 15
e[5][6] = 4

let dis = Array(11).fill(0)

for(let i = 0; i < n+1; i++) {
    dis[i] = e[keyPoint][i]
}

let book = Array(11).fill(0)
book[keyPoint] = 1

// Dijkstra Algorithm
for (let i = 1; i < n; i++) {
    // 找到離 keyPoint 點最近的頂點
    let min = infinity

    for(let j = 1; j < n+1; j++) {
        if (book[j] === 0 && dis[j] < min) {
            min = dis[j]
            u = j
        }
    }

    book[u] = 1
    for(let v = 1; v < n+1; v++) {
        if (e[u][v] < infinity) {
            if (dis[v] > dis[u] + e[u][v]) {
                dis[v] = dis[u] + e[u][v]
            }        
        }
    }
}

for(let i = 1; i < n+1; i++) {
    console.log(dis[i])
} 
```
