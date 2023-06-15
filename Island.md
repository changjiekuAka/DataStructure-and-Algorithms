# Island

### 问题

整形二维数组`arr`中分布着许多`1`，其余都是`0`，彼此相连的一群`1`构成一个岛屿，斜线不表示相连，求岛屿的数量

### 思路

遍历数组，遇到`1`进行感染`infect`，将`1`改成`2`

### 实现

```c++
void infect(vector<vector<int>>& arr,int i,int j)
{
    /******注意边界******/
    if(i > arr.size() || i < 0 || j > arr[0].size() || j < 0 || arr[i][j] != 1) return;
    
    arr[i][j] = 2;
    
    infect(arr,i - 1,j);
    infect(arr,i + 1,j);
	infect(arr,i,j + 1);
    infect(arr,i,j - 1);
}

int Island(vector<vector<int>> arr)
{
    int res = 0;
	for(int i = 0;i < arr.size();i++)
    {
        for(int j = 0;j < arr[0].size();j++)
        {
            if(arr[i][j] == 1)
            {
                res++;
                infect(arr,i,j);
            }
        }
    }
    return res;
}
```

### 总结

如果二维数组过大，那这个方法就不好使了，所以可以将数组分为两部分，再利用并查集的思想解决