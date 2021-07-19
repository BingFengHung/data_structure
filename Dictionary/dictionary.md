# Dictionary 字典

這個是一種不重複鍵值的資料結構

簡單來說就是一個鍵值對上一個值，由於鍵值是不可重複的，因此，如果有值要加到同一個值時，舊的值就會被覆蓋。

- set(key, value)：向字典加入新元素。
- remove(key)：
- has(key)
- get(key)
- clear()
- size()
- keys()
- values()

```js
class Dictionary {
    constructor() {
        this.items = {}
    }

    set(key, value) {
        this.items[key] = value;
    }

    remove(key) {
        if (this.has(key)) {
            delete this.items[key];
            return true;
        }

        return false;
    }

    has(key) {
        return key in this.items
    }

    get(key) {
        return this.has(key) ? this.items[key] : undefined;
    }

    clear() {
        this.items = {};
    }

    size(){
        return Object.keys(this.items).length;
    }

    keys(){
        return Object.keys(this.items);
    }

    values(){
        let values = [];

        for (let key in this.items) {
            if (this.has(key)) {
                values.push(this.items[key]);
            }
        }

        return values;
    }
}
```