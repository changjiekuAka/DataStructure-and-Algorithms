# Small sum

### 问题

遍历一个数组，每一个数左边比自身小的数累加起来，叫做一个数组的小和

### 思路

利用归并排序计算

> 注意：相等时右边区域的下标p2先走

### 实现

```C++
int smallSum(int arr[])
{
    int lenth = sizeof(arr) / sizeof(int);
    if(lenth < 2) return 0;
    
    return process(arr,0,lenth - 1);
}

int process(int arr[],int L,int R)
{
    if(L == R) return 0;
    
    int mid = (L + ((R - L) >> 1));
    
    return process(arr,L,mid) + process(arr,mid + 1,R) + merge(arr,L,mid,R);
}

int merge(int arr[],int L,int mid,int R)
{
    int help[R - L + 1];
    int p1 = L;
    int p2 = mid + 1;
    int res = 0;
    int i = 0;
    while(p1 <= mid&&p2 <= R)
    {
        res += arr[p1] < arr[p2] ? (R - p2 + 1)*arr[p1] : 0;
        help[i++] = arr[p1] < arr[p2] ? arr[p1++] : arr[p2++];
    }
    
    while(p1 <= mid)
    {
        help[i++] = arr[p1++];
    }
    
    while(p2 <= R)
    {
        help[i++] = arr[p2++];
    }
    
    for(i = 0;i < R - L + 1;i++)
    {
        arr[L + i] = help[i];
    }
    return res;
}
```

### 总结

相等时总是`p2`先走，直到找到比`arr[p1]`大的数；

根据 `p2`下标得到有多少个大于`arr[p1]`的数 * `arr[p1]` 得到 所在区域有多少个`arr[p1]`加入小和
