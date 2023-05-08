# MergeSort

### 思路

1. 将数组划分成**有序**(必须)的两个部分
2. 归并排序

### 实现

#### 将数组划分成有序的两个部分

```c++
void Process(int arr[],int L,int R)
{
    if(L >= R) return;
    
    int mid = (L + ((R - L) >> 1));		/******计算中间的数******/
    
    Process(arr,L,mid);				/******递归划分******/
    Process(arr,mid + 1,R);
    
    merge(arr,L,mid,R);				/******归并排序******/
}
```

#### 归并排序

```c++
void merge(int arr[],int L,int mid,int R)
{
    if(L >= R) return;
    
    int p1 = L;
    int p2 = mid + 1;
    int help[R - L + 1];
    int i = 0; 
    while(p1 <= mid && p2 <= L)
    {
        help[i++] = arr[p1] < arr[p2] ? arr[p1++]:arr[p2++];
    }
    while(p1 <= m)
    {
        help[i++] = arr[p1++]; 
    }
    while(p2 <= R)
    {
        help[i++] = arr[p2++];
    }
    for(i = 0;i < R;i++)
    {
        arr[L + i] = help[i];
    }
    
}
```

