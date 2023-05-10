# Reverse pair

### 问题

一个数组，其中一个数的左边有数大于其本身，则称它们形成逆序对，求逆序对的数量

### 思路

利用归并排序，综合小和问题解决

### 实现

```c++
int ReversePair(int arr[],int lenth)
{
   if(lenth < 2) return 0;
    
    return process(arr,0,lenth - 1);
}

int process(int arr[],int L,int R)
{
    if(L >= R) return 0;
    
    int mid = (L + ((R - L) >> 1));
    return process(arr,L,mid) + process(arr,mid + 1,R) + merge(arr,L,mid,R);
}

int merge(int arr[],int L,int mid,int R)
{
    int help[R - L + 1];
    int p1 = L;
    int p2 = mid + 1;
    int i = 0;
    int res = 0;
    while(p1 <= mid && p2 <= R)
    {
 		res += arr[p1] > arr[p2] ? (mid - p1 + 1) : 0;
        help[i++] = arr[p1] > arr[p2] ? arr[p2++] : arr[p1++];
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

归并排序，划分两个区域，根据左区域下标算出，左边有多少数大于右边。
