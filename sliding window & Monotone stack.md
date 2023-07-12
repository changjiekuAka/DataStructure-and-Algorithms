# sliding window & Monotone stack

## sliding window 

滑动窗口最常见的问题就是求局部空间内的最大值

### 问题

求数组中长度为3且相邻的数字和的最大值

### 思路

使用双向队列来控制局部空间里数据的进出，*尾巴进，头部出*

进：

