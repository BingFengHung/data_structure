# Union-find Algorithm 並查集

`並查集又稱為不相交集資料結構`

類似樹從葉節點慢慢合併，找到相應的根節點

ex。從班上小團體中，找到各自小團體的頭頭

- 合併時，遵守靠左原則
- 當有重複時，遵守擒賊先擒王的概念

```js

// people 人數, leads 線索
let people = 10
let leads = 9

let f = Array(people).fill(0).map((i, idx) => idx + 1)

function getF(f, v) {
    if (f[v] === v) {
        return v;
    } else {
        f[v] = getF(f, f[v])
        return f[v]
    }
}

function merge(f, v, u) {
    let t1 = getF(f, v)
    let t2 = getF(f, u)

    if(t1 !== t2) {
        f[t2] = t1
    }
}

// 開始合併線索
merge(f, 1, 2)
merge(f, 3, 4)
merge(f, 5, 2)
merge(f, 4, 6)
merge(f, 2, 6)
merge(f, 8, 7)
merge(f, 9, 7)
merge(f, 1, 6)
merge(f, 2, 4)

let sum = 0

for(let i = 0; i < people; i++) {
    if (f[i] === i) 
        sum+= 1
}

```