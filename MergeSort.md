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
    
    int mid = (L + (L+R)>>1);		/******计算中间的数******/
    
    Process(arr,L,mid);				/******递归划分******/
    Process(arr,mid + 1,R);
    
    merge(arr,L,mid,R);				/******归并排序******/
}
```

#### 归并排序