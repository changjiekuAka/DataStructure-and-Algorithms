# Common ancestor

### 最近公共祖先

### 思路

判断情况：

- 节点`o1`和节点`o2`的分别位于最近公共祖先的左右
- `o1`是最近公共祖先
- `o2`是最近公共祖先

### 实现

```c++
Node* GetCommonAncestor(Node* head,Node* o1,Node* o2)
{
    if(head == null || head == o1 || head == o2) return head;
    
    Node* dataLeft = GetCommonAncestor(head->left,o1,o2);
    Node* dataRight = GetCommonAncestor(head->right,o1,o2);
    /******处理情况1******/
    if(dataLeft != null && dataRight != null) return head;
    /******处理情况2.3******/
    return dataLeft == null ? dataRight : dataLeft;
}
```

### 总结

递归左右子树获取信息，处理情况
