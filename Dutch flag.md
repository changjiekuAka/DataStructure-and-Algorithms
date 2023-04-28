# '荷兰'国旗

### 问题

给一个数组，需要把其中的数字，根据`num`按三个区域划分开(**小于num**、**等于num**、**大于num**)

不要有序。

### 思路

> 注意：向前 == 向左  向后  == 向右

需要两个变量`under`、`upwords`，在`under`之前的为小于区域，在`upwords`之后为大于区域

利用变量`i` 遍历数组：

- `arr[i] < num`,交换`arr[i]`和小于区域的下一个数，小于区域往后移动，`i`++
- `arr[i] > num`,交换`arr[i]`和大于区域的前一个数，大于区域向前移动，`i`不变
- `arr[i] = num,i++`
- `i` 碰到 `upwords` 结束

### 实现

> 注意：under表示小于区域的下一个数据
>
> ​			upwords表示大于区域的前一个数据

```c++
void DutchFlag(int arr[],int num,int lenth) /******lenth为arr长度******/
{
    int under = 0;
    int upwords = lenth - 1;
    int i = 0;
    while(i <= upwords)
    {
        if(arr[i] < num)
        {
            swap(arr[i],arr[under]);
            under++;
            i++;
        }
        else if(arr[i] > num)
        {
            swap(arr[i],arr[upwords]);
            upwords--;
        }
        else
        {
            i++;
        }
    }
}
```

