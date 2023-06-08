# Empress N

### 问题

在一个二维数组中，皇后放置的位置不能与其他皇后在一行、在一列、在一斜线,求`num`个皇后在`num × num`的数组里全部摆放的方法个数

### 数据

`vector<int> arr` , `arr[k]` 表示在二维数组的第k行皇后放在第几列的下标

### 思路

依据`行`进行遍历，同时选取`列`的时候，判断有效性

### 实现

```c++
bool isValid(vector<int>& arr,int k,int j)
{
    for(int i = 0;i < k;i++)
    {
        if(arr[i] == j || abs(i - k) == abs(arr[i] - j)) return false;
    }
    return true;
}

int process(vector<int>& arr,int k,int num)
{
	if(k == num) return 1;/******终止行******/
    
    int res = 0;
    for(int i = 0;i < num; i++)
    {
        if(isValid(arr,k,i))
        {
            arr[k] = i;
            /******获取当前的选择下后续层返回的结果******/
            res += process(arr,k + 1,num);
        }
    }
    return res;
}

int func(int num)
{
    if(num < 1) return 0;
    vector<int> arr(num);
    return process(arr,0,num);
}
```

### 总结

也可以使用位运算解决



```c++
int process(int limit,int colnum,int leftdatalimit,int rightdatalimit)
{
    if(limit == colnum) return 1;
    
    int pos = limit & (~(colnum | leftdatalimit | rightdatalimit));
    int res = 0;
    while(pos != 0)
    {
        int mightrightdata = pos & (~pos + 1);
        pos -= mightrightdata;
        res += process(limit, colnum|mightrightdata,
                (leftdatalimit|mightrightdata) << 1,
               (rightdatalimit|mightrightdata) >>> 1);
    }
    return res;
}

int func(int num)
{
    if(num > 32 || num < 1) return 0;
    int limit = num == 32? -1:(1 << n) - 1;
    process(limit,0,0,0);
}
```

