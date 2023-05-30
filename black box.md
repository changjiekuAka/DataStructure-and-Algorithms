# black box

### 判断平衡二叉树

### 数据

使用`returnType`结构体：

- 一个节点的高度`height`
- 以此节点为根节点的树是否平衡`isBalance`

### 思路

利用左右递归返回的`returnType`，构建向上返回的`returnType`

### 实现

```java
public static class returnType
{
	
    public int height;
   	public boolean isBalance;
    
    public returnType(int hi,boolean isB) {
        height = hi;
        isBalance = isB;
    }
};

public static returnType isBBT(Node root)
{
    if(root == null) return new returnType(0,true);
    
    returnType Returnleft = isBBT(root.left);
    returnType Returnright = isBBT(root.right);
	
    int height = Math.max(Returnleft.height,Returnright.height) + 1;
    boolean isBalance = (Returnleft.isBBT && Returnright.isBBT) 
        && Math.abs(Returnright.height - Returnleft.height) < 2;
    return new returnType(height,isBalance);
}
```

### 判断平衡搜索二叉树

### 数据

结构体`returnType`：

- 以节点作为根节点的树是否平衡`isbst`
- 以节点作为的根节点的树的最大`key`
- 以节点作为的根节点的树的最小`key`

### 思路

利用左右递归返回的`returnType`，构建向上返回的`returnType`

### 实现

```java
public static class returnType{
	public boolean isbst;
    public int maxNum;
    public int minNum;
    
    public returnType(boolean is,int ma,int mi){
        isbst = is;
        maxNum = ma;
        minNum = mi;
    }      
};

public static returnType isBST(Node root)
{
    if(root == null) return new returnType(0,int.MIN,int.MAX);
    
    returnType Returnleft = isBST(root.left);
    returnType Returnright = isBST(root.right);
  	
    int Maxnum;
    int Minnum;
    if(Returnright != null)
    {
        Maxnum = Math.max(root.value,Returnright.maxNum);
        Minnum = Math.min(root.value,Returnright.minNum);
    }    
    if(Returnleft != null)
    {
        Maxnum = Math.max(root.value,Returnleft.maxNum);
        Minnum = Math.min(root.value,Returnleft.minNum);
    }    
    
    boolean isbst = false;
    
    if((Returnleft != null ? Returnleft.isbst && Returnleft.maxNum < root.value : true)
      && (Returnright != null ? Returnright.isbst && Returnright.minNum < root.value : true))
    {
        isbst = true;
    }
    
    return new returnType(isbst,Maxnum,Minnum);
}
```

### 总结

根据这两个结构的特性，提取判断所需的变量一起返回