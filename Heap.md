# Heap

### HeapInsert

```c++
void HeapInsert(int arr[],)
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
void Heapify(int arr[],int index,int heapsize)
{
	int left = 	index * 2;
    while(left < heapsize)
    {
        int largest = arr[left] > arr[left + 1]? left : left+1;
        
    }
}
```

