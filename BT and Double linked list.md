# BT and Double linked list

### 问题

将二叉树转换为双向循环列表

### 数据

`Node* head` 表示最终返回的结果

`Node* pre` 表示上一个处理节点

### 思路

利用中序遍历的思想，链接节点，并更新`pre`

### 实现

```c++
Node* head,Node* pre;
void dfs(Node* cur)
{
    if(cur == null) return;
    dfs(cur->left);
    
    /******走到最左节点******/
    if(pre == null) head = cur;
    else pre->right = cur;
    
    /******链接.更新******/
    cur->left = pre;
    pre = cur;
    
    dfs(cur->right);
}

Node* treeTodoubleList(Node* root)
{
    if(root == null) return null;
    dfs(root);
    head->left = pre;
    pre->right = head;
    return head;
}
```

> 总结自leetcode大佬 Krahets