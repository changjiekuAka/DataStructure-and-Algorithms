# KMP

### 问题

字符串匹配问题，问字符串 `str1`中是否存在连续的子串与字符串`str2`相等

### 思路

传统做法是依次遍历str1中的每个字符作为起始位置，看是否能凑出字符串str2.

KMP算法就是对传统做法的一种加速，对于有些节点是可以跳过的

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

vector<int> f2(string str)
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

