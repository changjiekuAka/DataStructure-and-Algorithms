# Successor node

### 问题

求二叉树里一个节点的后继节点

### 思路

判断情况：

节点有右子树：找右子树的最左节点

节点没有右子树：往上查找，但节点不能为父节点的左子树

### 实现

```c++
class Node
{
    public:
    Node* left;
    Node* right;
    Node* parent;
	Node():left(nullptr),right(nullptr),parent(nullptr){}   
};

Node* GetSuccessorNode(Node* root,Node* cur)
{
    if(!cur) return cur;
    
    if(cur->right) return GetLeftestNode(cur->right);
    Node* parent = cur->parent;
    while(parent != nullptr && parent->left != cur)
    {
        cur = parent;
        parent = cur->parent;
    }
    return parent;
}

Node* GetLeftestNode(Node* root)
{
    while(root->left)
    {
        root = root->left;
    }
    return root;
}
```

