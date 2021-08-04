# K-means 分群
將類似的資料分組再一起就是分群，而每一組分群叫做群集 (Cluster)

分類常用距離來做運算

K-means 分群
1. 先決定要分成幾組 k ，並隨機挑選 k 個點做為群集中心。
2. 將每一個點分類到離自己群集中心最近的點 (可用直線距離)，
3. 重新計算各組的群集中心 (常用平均值)

重複上述 2 3 步驟，直到群集不變，群集中心不動為止。

```js
// 假設要分為 3 群
// 資料點為 20 點

let group = 3
let data = 20

// 初始化資料點
let x = Array(data).fill(0).map(() => Math.round(Math.random() * 500))
let y = Array(data).fill(0).map(() => Math.round(Math.random() * 500))

// 初始化群集中心
let kx = Array(group).fill(0).map(() => Math.round(Math.random() * 500))
let ky = Array(group).fill(0).map(() => Math.round(Math.random() * 500))

// 計算兩點之間的距離
function distance(x, y, kx, ky) {
    return Math.sqrt(Math.pow(kx -x, 2) + Math.pow(ky - y, 2))
}

// 針對每筆資料分群
function cluster(x, y, kx, ky) {
    let team = [[], [], []]

    let middle = Number.MAX_VALUE
    let flag = 0

    for (let i = 0; i < data; i++) {
        for (let j = 0; j < group; j++) {
            dist = distance(x[i], y[i], kx[j], ky[j])

            if (dist < middle) {
                middle = dist
                flag = j
            }
        }

        team[flag].push([x[i], y[i]])

        middle = Number.MAX_VALUE
    }

    return team
}

// 對分群完的元素找出新的群集中心
function clusterCenter(team, kx, ky) {
    let sumx = 0
    let sumy = 0

    let new_seed = []

    for(let i in team) {
        if (team[i].length === 0) {
            new_seed.push([kx[i], ky[i]])
        }
        else {
            for(let j of team[i]) {
                sumx += j[0]
                sumy += j[1]
            }

            new_seed.push([sumx/team[i].length, sumy/team[i].length])
        }


        sumx = 0
        sumy = 0
    }

    let nkx = []
    let nky = []

    for(let i of new_seed) { 
        nkx.push(i[0])
        nky.push(i[1])
    }
    
    return [nkx, nky]
}


// k-means 分群

function kmeans(x, y, kx, ky, fig) {
    let team = cluster(x, y, kx, ky)
    
    let [nkx, nky] = clusterCenter(team, kx, ky);

    let cx = []
    let cy = []

    for (let i in team) {
        for (let j of i) {
            cx.push([j[0], nkx[i]])
            cy.push([j[1], nkx[i]])
        }

        cx = []
        cy = []
    }

    // 判斷群集中心是否不再變動
    if (JSON.stringify(nkx) === JSON.stringify(kx) && JSON.stringify(nky) === JSON.stringify(ky)) 
    {
        return;
    }
    else {
        fig += 1
        kmeans(x, y, nkx, nky, fig);
    }
}

kmeans(x, y, kx, ky, 0)
```