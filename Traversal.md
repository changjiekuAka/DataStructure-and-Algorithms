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

## 后续

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