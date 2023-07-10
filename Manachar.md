# Manacher

### 问题

寻找字符串中的最长回文串

### 传统做法

- 字符串首字符前加一个特殊字符 `‘#’` 末尾字符加一个特殊字符 `‘#’` 相邻字符间也加上特殊字符 `‘#’`
- 遍历字符串，除特殊字符外，以每个字符作为回文字符串的中心向外扩张

#### 思考

很明显这种做法的时间复杂度是很高的，所以采用`manacher`进行提速

### 提速

#### 数据

记录数据`R`表示目前最长回文串的的半径

记录数据`M`表示目前最长回文串的中心

数组`parr`存储每个字符为中心的最长回文串的半径

### 思路

根据遍历字符下标`i`和`R`的关系分为以下情况

1. `i`在`R`范围外，则自己往外扩
2. `i`在`R`范围内，根据以`M`做对称点的`i'`情况分为三种情况

- `parr[i']`在`R`范围内，但不与`R`边缘位置重叠，则`parr[i] = parr[i']`
- `parr[i']`超出R范围，则`parr[i] = R - i`
- `parr[i']`在`R`范围内，与`R`边缘位置重叠，也是自行扩，有一段距离不用判断: `R - i`

### 实现

```c++
string f1(string str)
{
    string res;
    
	for(int i = 0;i < str.size() * 2 + 1;i++)
    {
        res += i & 1 ? str[i / 2] : '#';
    }
    return res;
}

int f2(string str)
{
    if(str.size() == 0) return 0;
    int R = -1;
    int M = -1;
    string pstr = f1(str);
    int* parr = new int(pstr.size());
    int Rmax = INT32_MIN;
    for(int i = 0;i < pstr.size();i++)
    {
        /******不用判断的半径******/
        int parr[i] = R > i ? min(parr[2 * M - i],R - i) : 1;
        
        while(i + parr[i] < pstr.size() && i - parr[i] > -1)
        {
            if(str[i + parr[i]] == str[i - parr[i]])
            {
                parr[i]++;
            }
            else break;
        }
    	
        if(parr[i] + i > R)
        {
            R = i + parr[i];
            M = i;
        }
        Rmax = max(Rmax,parr[i]);
    }
    delede[] parr;
    return Rmax - 1;
}
```

### 思考

#### parr[i'] 在R范围内

![image-20230702162439201](C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230702162439201.png)

`R`范围内已是回文串且以`M`为中心点，所以`M`做对称点的`i'`的半径结果，就是`i`的半径结果

#### parr[i'] 超出R范围内

![image-20230702162700124](C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230702162700124.png)

i的半径结果为`R - i`，不可能为更大

##### R - i 为什么不可能更大

![image-20230702163403442](C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230702163403442.png)

如图，假设i开始还可以往外扩，则`？ =   b` ；以M为中心，`?` 的对称点也为`b`，那`R`的值应该更大才对，可是`R`之前并没有扩到那么大，所以假设不成立

### parr[i'] 在R范围内，但与R重叠

![image-20230702164802244](C:\Users\ZZZXXXJJ\AppData\Roaming\Typora\typora-user-images\image-20230702164802244.png)

此情况下`i`是可以往外扩的，不会影响R值，可以用上面的方法印证

### 总结

不同情况下，扩与不扩分析，需要理解清楚
