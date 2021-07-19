# Queue 佇列
Queue 與 Stack 很類似，不過 Queue 為先進先出 (LIFO)

主要就是像排隊那樣，先進來的人先進行服務，服務完之後就走，後面的人再補上。

以下是 Queue 的介面
- enqueue
- dequeue
- isEmpty
- size
- clear

```js
class Node
{
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class Queue
{
    constructor() {
        this.head = null;
        this.tail = null;
        this.count = 0;
    }

    print() {
        let ptr = this.head;

        while(ptr) {
            console.log(ptr.data);
            ptr = ptr.next;
        }
    }

    enqueue(data) {
        let node = new Node(data);

        if (this.head === null) {
            this.head = node;
            this.tail = node;
        } else {
            this.tail.next = node;
            this.tail = node;
        }

        this.count++;
    }

    dequeue() {
        let ptr = this.head;

        if (ptr != null) {
            this.head = ptr.next;    
            ptr = null;
            this.count--;
        }
    }

    isEmpty() {
        return this.count === 0;
    }

    size() {
        return this.count;
    }

    clear() {
        let ptr = this.head;

        while(this.head) {
            this.dequeue();
        }
    }
}
```