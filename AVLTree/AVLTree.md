# AVL Tree
AVL Tree (高度平衡樹)，他主要要調整樹的結構，來讓樹保持平衡，不會導致樹過度傾斜 (不平衡)

要達到平衡，需透過以下幾項方式來達成：
1. 計算節點高度
2. 計算 Balance Factor
3. 理解什麼是高度平衡樹

### 節點的高度
Height of node: Length of the longest path from it to the leaf height = max(leftChildHeight, rightChildHeight) + 1

### Balance Factor of T
For node T in a binary search tree is defined to be HL-HR where HL and HR respectively, are the heights of the left and right subtree of T.

BF(T) < -1： 右子樹比較重，需要往左邊調整
-1 <= BF(T) <= 1>： 平衡，暫時不調整
BF(T) > 1：左子樹比較重，需要往右邊調整

### 高度平衡
要計算二元樹是否平衡，就是計算 root 左右節點的高度，得到高度後相減，如果得到的結果 < -1 或 > 1，則表示不平衡。

在遇到不平衡情況時，需要調整數的節點，這邊稱為Rotation，Rotation有個很重要的目的， rotation 前與後的樹，整個 tree的 in-order traversal 相同 。

旋轉共分為四種類型，都是左旋轉與右旋轉的變化組合
BF > 1，表示左邊較重，需要做 right rotation

BF < -1，表示右邊較重，需要做 left rotation

1. LL
2. LR
3. RR
4. RL

```js
class TreeNode {
    constructor(data) {
        this.left = null;
        this.right = null;
        this.data = data;
        this.height = 0;
    }

    compareTo(data) {
        if (this.data > data) return 1;
        else if (this.data < data) return -1;
        else 0;
    }

    getHeight() {
        return this.height;
    }

    setHeight(height) {
        this.height = height;
    }

    getLeftNode() {
        return this.left;
    }

    getRightNode() {
        return this.right;
    }

    setLeftNode(node) {
        this.left = node;
    }

    setRightNode(node) {
        this.righ = node;
    }

    getData() {
        return this.data;
    }

    setData(data) {
        this.data = data;
    }
}

class AVLTree {
    constructor() {
        this.root = null;
    }

    

    findElement(data) {
        if(this.getRoot() === null) 
            return null;
        return this.findElement2(data, getRoot())
    }

    findElement2(data, node) {
        if (node === null)
           return null;
        
        if (node.getData().compareTo(data) < 0) 
            return this.findElement2(data, node.getRightNode())
        else if (node.getData().compareTo(data) > 0) 
           return this.findElement2(data, node.getLeftNode());
        else return node;
    }

    getRoot() {
        return this.root;
    }

    deleteElement(data) {
        if(this.getRoot() === null)
           return null;
        this.root = this.deleteElement2(data, this.getRoot())
        return this.root;
    }

    deleteElement2(data, node) {
        if (node === null)
           return null;
        
        if(node.compareTo(data) < 0) {
            node.setRightNode(this.deleteElement2(data, node.getRightNode()));
        } else if (node.compareTo(data) > 0) {
            node.setLeftNode(this.deleteElement2(data, node.getLeftNode()));
        } else {
            if (node.getLeftNode() === null && node.getRightNode() === null)
               return null;
            else if (node.getLeftNode() === null)
               return node.getRightNode();
            else if (node.getRightNode() === null)
               return node.getLeftNode();
            else {
                let leftMaxValueTreeNode = this.findMaxValueNode(node.getLeftNode());

                let tempData = node.getData();
                node.setData(leftMaxValueTreeNode.getData())

                leftMaxValueTreeNode.setData(tempData);

                node.setLeftNode(deleteElement2(data, node.getLeftNode()))
            }
        }

        this.updateNodeHeight(node);

        return this.updateTreeBalance(node);
    }

    insertElement(data) {
        console.log(data)
        if(this.getRoot() === null) {
           this.root = new TreeNode(data); 
        }
        else {
           this.root = this.insertElement2(data, this.getRoot()) 
        }
    }

    insertElement2(data, currentNode) {
        if (currentNode === null)
           return new TreeNode(data)
        
        if(currentNode.compareTo(data) <= -1) {
            currentNode.setRightNode(this.insertElement2(data, currentNode.getRightNode()))
        } else {
            currentNode.setLeftNode(this.insertElement2(data, currentNode.getLeftNode()))
        }

        this.updateNodeHeight(currentNode)
        return this.updateTreeBalance(currentNode)
    }

    traverse() {
        this.traverse2(this.getRoot())
    }

    traverse2(node) {
        if(node === null) return;
        this.traverse2(node.getLeftNode())

        console.log(" -> " + node.getData())
        this.traverse2(node.getRightNode())
    }

    updateTreeBalance(node) {
        let bf = this.getBalanceFactor(node)

        if(bf > 1) {
            if (node.getLeftNode() !== node && node.getLeftNode().getLeftNode() !== null) {
                return this.rightRotation(node)
            } else {
                node.setLeftNode(this.leftRotation(node.getLeftNode()));
                return rightRotation(node)
            }
        } else if (bf < -1) {
            if (node.getRightNode() !== null && node.getRightNode().getRightNode() !== null) {
                return leftRotation(node)
            } else {
                node.setRightNode(this.rightRotation(node.getRightNode()))

                return leftRotation(node)
            }
        }

        return node;
    }

    getNodeHeight(node) {
        if (node === null) return -1;
        return node.getHeight();
    }

    getBalanceFactor(node) {
        if (node === null)
           return 0;
        return this.getNodeHeight(node.getLeftNode()) - this.getNodeHeight(node.getRightNode());
    }

    updateNodeHeight(node) {
        if (node === null) return;
        node.setHeight(Math.max(this.getNodeHeight(node.getLeftNode()), this.getNodeHeight(node.getRightNode())) + 1);
    }

    rightRotation(node) {
        console.log("Perform right rotation on node: " + node.getData())
        let leftChild = node.getLeftNode();
        let tempNode = leftChild.getRightNode();

        node.setLeftNode(tempNode)
        leftChild.setRightNode(node);

        updateNodeHeight(node);

        updateNodeHeight(leftChild);

        return leftChild;
    }

    leftRotation(node) {
        console.log("Perform left rotation on node: " + node.getData())
        let rightChild = node.getRightNode();
        let tempNode = rightChild.getLeftNode();

        node.setRightNode(tempNode);
        rightChild.setLeftNode(node);

        this.updateNodeHeight(node);
        this.updateNodeHeight(rightChild);

        return rightChild;
    }

    findMaxValueNode(node) {
        if (node === null) return null;

        if(node.getRightNode() !== null)
           return this.findMaxValueNode(node.getRightNode())
        return node;
    }
}



let tree = new AVLTree();

tree.insertElement("APR");
tree.insertElement("AUG");
tree.insertElement("DEC");
tree.insertElement("FEB");
tree.insertElement("JAN");
tree.insertElement("JULY");
tree.insertElement("JUNE");
tree.insertElement("MAR");
tree.insertElement("MAY");
tree.insertElement("NOV");
tree.insertElement("OCT");
tree.insertElement("SEPT");
tree.traverse();
tree.deleteElement("APR");
tree.deleteElement("JAN");
tree.deleteElement("FEB");
tree.traverse();
```

參考：
https://josephjsf2.github.io/data/structure/and/algorithm/2019/06/22/avl-tree.html