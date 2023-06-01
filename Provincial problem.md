# Provincial problem

### 问题

给定一个二维数组 `vector<vector<int>> arr`,`arr[i][j]= 1`表示 `i` 省和 `j` 省相连，`0` 则不相连，求省份个数(相连的省叫做省份)

### 数据

`vector<int> ufs` 用于模拟并查集

### 思路

相连则合并，最终统计

### 实现

```c++
int GetProvince(vector<vector<int>>& arr)
{
    vector<int> ufs(arr.size(),-1);
    
    auto FindRoot = [&ufs](int x){
        while(ufs[x] >= 0)
        {
            x = usf[x];
        }
        return x;
    };
    
    for(int i = 0;i < arr.size();i++)
    {
        for(int j = 0;j < arr[i].size();j++)
        {
            if(arr[i][j])
            {
                int root1 = FindRoot(i);
                int root2 = FindRoot(j);
                if(root1 != root2)
                {
                    ufs[root1] += usf[root2];
                    usf[root2] = root1; 
                }
            }
        }
    }
    
    int res = 0;
    for(auto num:ufs)
    {
        if(num < 0) res++;
    }
    return res;
}
```

### 总结

这是不用库函数的做法，实际两者的思想都一样