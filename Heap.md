# Heap

### HeapInsert

```c++
/******index往上调整******/
void HeapInsert(int arr[],int index)
{
	while(index > 0)
    {
        swap(arr,index,(index - 1)/2);
        index = (index - 1)/2;
    }
}
```

### Heapify

```c++
/******index往下调整******/
void Heapify(int arr[],int index,int heapsize)
{
	int left = 	index * 2 + 1;
    while(left < heapsize)
    {
        int largest = left + 1 < heapsize && arr[left] > arr[left + 1] ? left : left + 1;
        largest = arr[index] > arr[largest] ? index:largest;
        if(index == largest) break;
        
        swap(arr,arr[largest],arr[index]);
        index = largest;
        left = index * 2 + 1;
    }
}
```

> 注意：堆中一个数变大了就用HeapInsert调整
>
> ​			堆中一个数变小了就用Heapify调整
