# Stack 堆疊
堆疊是一種遵循先進後出 (LIFO)的原則。

一個簡單的範例就是碟盤子，洗好的盤子會一個一個往上疊；當要使用盤子時，會先從最上面那一個取用。

## 堆疊操作介面
- push
- pop
- peek
- isEmpty
- clear
- size


```js
class Node
{
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class Stack
{
    constructor()
    {
        this.top = null;
        this.size = 0;
    }

    print() {
        let ptr = this.top;
        while(ptr) {
            console.log(ptr.data)
            ptr = ptr.next;
        }
    }

    push(data) {
        let node = new Node(data);
        node.next = this.top;
        this.top = node;
        this.size++;
    }

    pop() {
        if (this.top != null) {
            this.top = this.top.next;
            this.size--;
        }
    }
    peek() {
        return this.top.data;
    }
    isEmpty() {
        return this.size === 0;
    }
    clear() {
        while(this.top) {
            this.pop()
        }
    }

    sizes() {
        return this.size;
    }
}

```