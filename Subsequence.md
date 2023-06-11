# Subsequence

### 问题

求一个字符串的子序列

### 思路

对于每个字符都有 选择 和 不选择 ，根据这两个方向进行递归

### 实现

```c++
void GetSubsequence(string str,int k)
{
	if (k == str.size())
	{
		cout << str << endl;
		return;
	}
	func(str, k + 1);/******选择第k个字符******/
	char tmp = str[k];
	str[k] = 0;
	func(str, k + 1);/******不选择第k个字符******/
	str[k] = tmp;
}
```

### 总结

提前保存第k个字符，保证不破坏原始字符串，同样也是保证其他递归路线正常执行。

也可以使用STL容器保存字符选择的结果，思路都是一样的。