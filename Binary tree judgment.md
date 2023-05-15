# Binary tree judgment

### 判断完全二叉树

### 思路

使用层序遍历的思想

- 遇到节点左为空且右不为空，则不是
- 遇到一个叶子节点，其后必全是叶子节点，否则不是

### 实现

```c++
bool isCBT(Node* root)
{
    if(root != null)
    {
        queue<Node*> Nodeque;
        Nodeque.push(root);
        bool leaf = false;
        while(!Nodeque.empty())
        {
            Node* Front = Nodeque.front();
            Nodeque.pop();
            
            /******遇到子节点后，后续必全是子节点******/
            if(leaf && (Front->left != null || Front->right != null))
            {
                return false;
            }
            /******左为空，又不为空，不是完全二叉树******/
            if(Front->left == null&&Front->right != null)
            {
                return false;
            }
            
            if(Front->left) Nodeque.push(Front->left);
            if(Front->right) Nodeque.push(Front->right);
            /******遇到第一个子节点******/
            if(!Front->left && !Front->right) leaf = true;
        }
    }
    return true;
}
```

### 判断搜索二叉树

### 数据

使用`preValue`表示左子树最后处理的数

### 思路

- 使用中序遍历的思想
- 比较`preValue`和`root->value`

### 实现

```c++
static int preValue = -1;
bool isSBT(Node* root)
{
    if(root == null) return true;
    
    bool isSBTleft = isSBT(root->left);
    if(!isSBTleft) return false;
    
    if(root->value <= preValue) return false;
    preValue = root->value;
    
    return isSBT(root->right);
}
```

## 总结

需要结合这两种二叉树的特性进行判断，考验对其结构的理解