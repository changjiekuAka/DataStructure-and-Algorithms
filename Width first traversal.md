# Width first traversal

## 哈希表

### 数据

使用变量`curLevel` 记录当前遍历层数 ；`curLevelnode` 记录当前层的节点个数 

哈希表`Level`记录节点与它所在层数的对应关系

队列`NodeSeq`实现层序遍历

### 思路

将根节点和它所在第一层入哈希表`Level`

根节点入队列`NodeSeq`，进行层序遍历

每次`pop`节点`Front`，比较`Front`所在层数与`curLevel`

### 实现

```c++
void WidthMax(Node* root)
{
    if(root != nullptr)
    {
        queue<Node*> NodeSeq;
        int curLevel = 1;
        int curLevelnode = 0;
        unordered_map<Node*,int> Level;
        int width = -1;
        
        Level[root] = 1;
        NodeSeq.push(root);
        
        while(!NodeSeq.empty())
        {
            Node* Front = NodeSeq.front();
            NodeSeq.pop();
        	if(Level[Front] == curLevel)
            {
                curLevelnode++;
            }
            else
            {
                width = max(width,curLevelnode);
                curLevel++;
                curLevelnode = 1;
            }
            
            if(Front->left) 
            {
                NodeSeq.push(Front->left);
                Level[Front->left] = curLevel + 1;
            }
            if(Front->right)
            {
                NodeSeq.push(Front->right);
                Level[Front->right] = curLevel + 1;
            }
        }
        cout << width << endl;
    }
}
```

### 总结

使用`Hashmap`记录当前节点所在层数，根据层序遍历的顺序了解节点所在层的变化



## 有限变量

### 数据

`Node* curEnd` 表示当前层最后一个节点，`Node* curNextEnd` 表示下一层的最后一个节点

`NodeSeq` 层序遍历所用队列

### 思路

首先把`curEnd`设为根节点`root`

`pop`节点`Front`，比较`Front`和`curEnd`

`curNextEnd`设为每次新入栈的节点

### 实现

```c++
void WidthMax(Node* root)
{
	if(root != nullptr)
    {
        Node* curEnd = root;
        Node* curNextEnd = nullptr;
        int curLevelnode = 0;
        int res = -1;
        queue<int> NodeSeq;
        while(!NodeSeq.empty())
        {
            Node* Front = NodeSeq.front();
            NodeSeq.pop();
            if(Front == curEnd)
            {
                curLevelnode++;
                res = max(res,curLevelnode);
                curEnd = curNextEnd;
                curNextEnd = nullptr;
            }
            else
            {
                curLevelnode++;
            }
            
            if(cur->left)
            {
                NodeSeq.push(cur->left);
                curNextEnd = cur->left;
            }
            
            if(cur->right)
            {
                NodeSeq.push(cur->right);
                curNextEnd = cur->right;
            }
        }
        return res;
    }
}
```

### 总结

利用`curEnd`判断，遍历节点是否抵达一层的最后节点，并在入队列时更新下一层的最后节点。