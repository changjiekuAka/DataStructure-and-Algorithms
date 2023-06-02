# Median

### 问题

求数据流中的中位数

### 数据

使用大堆和小堆

### 思路

使用大堆小堆将数据分割开来

### 实现

```c++
int GetMedian(int arr[],int length)
{
	priority_queue<int,vector<int>,less<>> minHeap;
	priority_queue<int,vector<int>,greater<>> maxHeap;
	
	for(int i = 0;i < length; i++)
	{
		if(maxHeap.empty() || arr[i] <= maxHeap.top())
		{
			maxHeap.push(arr[i]);
		}
		else
		{
			minHeap.push(arr[i]);
		}
		
		if(maxHeap.size() - minHeap.size() > 1)
		{
			minHeap.push(maxHeap.top());
			maxHeap.pop();
		}
		else
		{
			maxHeap.push(minHeap.top());
			minHeap.pop();
		}
	}
	return maxHeap.size() > minHeap.size() ? maxHeap.top() : minHeap.top();	
}
```

