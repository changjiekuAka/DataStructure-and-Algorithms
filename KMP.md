# KMP

### 问题

字符串匹配问题，问字符串 `str1`中是否存在连续的子串与字符串`str2`相等,存在返回子串的起始位置，否则返回`-1`

### 思路

传统做法是依次遍历`str1`中的每个字符作为起始位置，看是否能凑出字符串`str2`.

`KMP`算法就是对传统做法的一种加速，对于有些节点是可以跳过的

### 数据

数组`next` ： 用于存储下标`i`前面长度为`i-1`的字符串 前缀 和 后缀相等的最长长度

### 实现

```c++
int f1(string str1,string str2)
{
    if(str1.size() < str2.size()) return 0;
    
    vector<int> arr = GetNextArr(str2);
    int i1 = 0 , i2 = 0;
    while(i1 < str1.size())
    {
        if(str1[i1] == str2[i2])
        {
            i1++;
            i2++;
        }
        else if(next[i2] == -1)
        {
            i1++;
        }
        else
        {
            i2 = next[i2];
        }
    }
    return i2 == str2.size() ? i1 - i2 : -1;
}

vector<int> GetNextArr(string str)
{
    if(str2.size() == 1)
    {
        return vector<int>(1,-1);
    }
    
    vector<int> next(str.size());
    next[0] = -1;
    next[1] = 0;
   	int cn = 0;
    int i = 2;
    while(i < str.size())
    {
        if(next[cn] == str[i - 1])
        {
            next[i++] = ++cn;
        }
        else if(cn > 0)
        {
            cn = next[cn];
        }
        else
        {
            next[i++] = 0;
        }
    }
    return next;
}
```

### 思考

#### 如何做到加速

![image-20230623113455960](C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230623113455960.png)

当`i1`位置字符和`i2`位置字符不相等时，`i2`来到前 `i2 - 1` 的 **前缀和后缀相等的最长长度**的下一个位置也就是next[i2].

因为`i1`前的字符和`i2`前的字符相等，可得到如图的切割，比较`i1`和`k`的字符，相当于`str1`的比较起始位置来到切割位置

#### 为何可以跳过切割位置前面的字符

<img src="C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230623115033627.png" alt="image-20230623115033627" style="zoom:50%;" />

假设`S`位置起始可以凑出字符串`str2`，那`S`到`i1-1`的长度`A`应与`str2`中的长度`B`中的字符相等。

由于`i1`前的字符和`i2`前的字符相等，则相等长度`C`和`A`中的字符应该相等，`=》A=B=C` 。

`B=C`，得到新的前缀和后缀相等的最长长度，违背了我们之前算出的结果，所以`S`起始不成立
