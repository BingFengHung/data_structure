# data_structure
Learn data structure concept

## 前言
主要以 JavaScript 資料結構演算法與實作這本書進行筆記

所謂資料結構 (Data Structe)，就是對於要解決的問題，為了配合演算法的運算，考慮如何運用變數，好讓所要解決問題的資料，在程式內有結構化的存放，以方便演算法的計算，並提升演算法的效率。

## 常用的資料結構
|資料結構|說明|
|---|---|
|陣列|是一種只需使用一個名稱卻可以存放大量資料的變數|
|鏈結串列|是一種比陣列更有彈性，且不必事先宣告大小的變數|
|堆疊|是一種類似蝶盤子的資料型態，取出與放入資料都在同一邊執行。|
|佇列|是一種類似排隊購物的資料型態，出入扣在不同邊執行|
|樹狀結構|是一種類似族譜的資料型態，非線性集合，有階層關係|
|圖形結構|是一種類似地圖的資料型態，有目標地與路徑，為非線性組合。|
|排序|是一種對資料排列的技術，有遞增或遞減兩種方式|
|搜尋|是一種尋找資料的技術。|


## 抽象資料型別
抽象資料型別 (Abstract Data Type, ADT) 主要就是定義出各種資料結構的介面，並未包含實作。

在電腦科學中，抽樣資料型態是一種理論上的觀念，他主要是用於設計與分析演算法、資料結構及軟體系統當中，而一個資料結構通常定義了`資料型別(values)`和操作方式`(operations)`，舉例來說，整數 (Integer) 就是一種抽象資料型態，他定義了在這個 ADT 底下，其資料型態(value) 為整數 (-2, -1, 0, 1, 2 等)且操作方式(operation) 有加減乘除等。

此外，抽象資料型泰的這個概念並沒有限定於特定的程式語言，換言之，不同的程式語言都可以實作抽象資料型別的概念，而且單一種ADT也可透過多種不同的方式來進行實作。

ex:
- List：get(), insert(), remove()
- Stack：push(), pop(), isEmpty(), isNull()
- Queue：enqueue(), dequeue(), size(), peek()

## 排序演算法
- 氣泡排序法： 這個排序方法，是透過將較小元素搬到陣列開始，較大的元素則慢慢浮往陣列的最後。
- 插入排序法： 插入時，會`由右而左`比較，當碰到比當前欲插入的值要小時，往左移動插入；若值比較大，則往右插入。
- 選擇排序法： 選擇排序法是從陣列中，挑出最小的一個元素，然後與第一個元素交換，接著再從剩下陣列元素中，找出最小的與第二個元素做交換，以此類推，直到結束。
- 合併排序法： 先將陣列元素拆開成一個個小陣列，再將這些小陣列進行比較，合併為一個大陣列。
- 快速排序法： 設定一個基準點，並從陣列的左邊找到比基準點大的值，以及從陣列右邊找出比基準點小的點，找到後，將兩點交換，重複上述步驟，在兩點指標交叉時停下，接這各自在重複上述步驟解決左陣列與右陣列。
