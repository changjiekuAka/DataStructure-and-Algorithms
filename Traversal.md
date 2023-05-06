# Traversal

> 注意stack弹出的顺序决定是如何遍历

## 先序

### 思路

1. 取二叉树根节点入栈
2. `pop`栈顶数据`Top`
3. 先入`Top`右，再入`Top`左

重复2、3步骤，直到栈为空

### 实现

```c++
void PreOrderUnRecur(Node* root)
{
    if(root != null)
   	{
		stack<Node*> cons;
    	cons.push(root);
    	while(!cons.empty())
    	{
        	Node* Top = cons.top();
        	cons.pop();
        	cout << Top->value << " ";
    	    if(Top->right) cons.push(Top->right);
            if(Top->left) cons.push(Top->left);
	    }
    }
}
```

## 后序

### 思路

使用两个栈 `cons` 、`help`

1. 根节点入栈`cons`
2. `pop`数据`Top`到`help`
3. 先入`Top`左，再入`Top`右，均入`cons`

重复步骤2、3，直到cons没有数据，依次拿出`help`中的数据

### 实现

```c++
void PostOrderUnRecur(Node* root)
{
    if(root != null)
    {
        stack<Node*> cons;
        stack<Node*> help;
        cons.push(root);
        while(!cons.empty())
        {
            Node* Top = cons.top();
            cons.pop();
            help.push(Top);
            if(Top->left) cons.push(Top->left);
            if(Top->right) cons.push(Top->right);
        }
        while(!help.empty())
        {
            Node* val = help.top();
            help.pop();
            cont << val->value << " ";
        }
    }
}
```

## 总结

**栈入**数据的顺序是和**弹出**时的顺序是**相反**的。

**弹出的顺序**即决定是**先序遍历**还是**后续遍历**。

> 先序遍历 -- -- 头左右 -- -- 要求入栈顺序：头右左
>
> 后序遍历 -- -- 左右头 -- -- 要求入栈顺序：头左右 -- -- 得到出栈顺序：头右左 -- -- help反转出栈顺序

## 中序

### 思路

首先根节点的所有左节点入栈

- `pop`节点`Top`，把`Top`节点的右子树的左节点入栈

重复上面的步骤，直到栈为空

### 实现

```c++
void InOrderUnRecur(Node* root)
{
    if(root != nullptr)
    {
        stack<Node*> cons;
        Node* cur = root;
        while(!cons.empty() || cur != nullptr)
        {
            if(cur == nullptr)
            {
                Node* Top = cons.top();
                cons.pop();
                cout << Top->value <<" ";
                cur = Top->right;
            }
            else
            {
                cons.push(cur);
                cur = cur->left;
            }
        }
    }
}
    
```

### 总结

对于一个节点`Node`和它的左节点`LNode`、右节点`RNode`，出栈的顺序： `LNode` -> `Node` -> `RNode`，也可以说是处理这个节点的顺序