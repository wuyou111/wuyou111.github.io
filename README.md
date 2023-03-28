# 力扣笔记

## 力扣第1784题

求解字符串是否包含某子串

- c语言：s.strstr(str1,str2) 
str1为母串，str2为子串，返回char* 
找出str2字符串在str1字符串中第一次出现的位置（不包括str2的串结束符）。返回该位置的指针，如找不到，返回空指针NULL

- C++: s.find("01")

- JAVA: s.contains("01")



## 力扣第1790题

- python zip函数 zip(\[iterable, ...\])  
示例代码：
```python
list1 = [1,2,3]
list2 = ['a','b','c']
for index,(x,y) in enumerate(zip(list1,list2)):
    print(index,x,y)
# 输出：    
# 0 1 a
# 1 2 b
# 2 3 c
```

## 力扣第1791题

- python collections.Counter、.most_common(k)


## 力扣第1796题

- python 1<2<3 语法糖
示例：  
```python
1<2<3
1<2 and 2<3
# 输出：
# True
# True
# 也即： 1<2<3 等价于 1<2 and 2<3
```
- 注意严格不等于
- 注意O(n)时间复杂度求序列前k大个数，根堆思想，即：新元素入堆-->调整根堆


## 力扣第704题 
二分查找  

- 注意right初值 是len(nums) 还是len(nums)-1
- 注意循环条件是left<right 还是left<=right
- 注意更新left和right时，left=middle+1,而right=middle-1 还是right=middle
- 注意保持循环变量一致原则，也即区间一致  
  
  
两个版本示例代码  
> 左闭右闭
```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = (left + right) / 2
            if nums[middle] > target:
                right = middle - 1
            elif nums[middle] <target:
                left = middle + 1
            else:
                return middle
        return -1
```
> 左闭右开
```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums)
        while left < right:
            middle = (left + right) / 2
            if nums[middle] > target:
                right = middle
            elif nums[middle] <target:
                left = middle + 1
            else:
                return middle
        return -1
```

## 力扣第27题 
移除元素
- 双指针 fast 和 slow，fast遍历数组，slow作为“新”数组的下标


## 力扣第977题
有序数组的平方
- 双指针的使用，思路来源，有序数组元素平方后，一定是两头大中间小的，以中间小为界，即为两个有序数组归并，采用双指针
- 注意需倒序放置平方后的元素以保证升序而不是降序

## 力扣第2902题  
翻转数位
- 采用滑窗思路，从低位往高位滑动，左边界遇1伸展，第一次遇0用掉翻转机会继续前进，再次遇0左边界停止，右边界缩至上次翻转时的后一位；重复以上步骤到左边界越界，记录每次的max长度输出。
- python bin(n & 0x ffffffff)
- 采用bin()函数转换为二进制的字符串时，加上一个前导零规避边界情况
- 优化：采用位运算，n & (1<<left) 获取left指向位置的0或1
- python 连续赋值： right = left = 0

## 力扣第209题
长度最小的子数组
- python 最大整型：sys.maxsize
- 采用滑窗思路，从左往右滑，右边界向右滑动直到窗口内的 元素和>=target，再右滑左边界直到窗口内的 元素和<target，重复以上步骤到右边界越界，记录每次满足条件的min子数组长度
- 为什么采用滑窗？滑窗是对暴力解法的优化。暴力枚举：两层循环枚举所有满足条件的子数组，也即外层循环控制子数组的起点，内层循环遍历找到以nums\[i\]为起点的满足条件的最小子数组。重点来了：暴力枚举以数组所有元素为起点的满足条件的子数组，子数组的**右边界是递增的**  
举例说明：  
nums=\[1,2,3,4,5\],target=6。暴力枚举时，  
外层第一次循环找到的以第一个元素1为起点的满足条件的长度最小子数组为\[1,2,3\]，  
外层第二次循环找到的以第二个元素2为起点的满足条件的长度最小子数组为\[2,3,4\],  
外层第三次循环找到的以第三个元素3为起点的满足条件的长度最小子数组为\[3,4\],
外层第四次循环找到的以第四个元素4为起点的满足条件的长度最小子数组为\[4，5\]
即满足条件的子数组的右边界index是递增的，这样：在第一次滑动右边界到满足条件停下来时，和暴力枚举一样，找到的是以第一个元素为起点的满足条件的子数组；接下来若是暴力枚举，子数组起点应设置为第二个元素，但由于满足条件的子数组的右边界index是**递增**的，所以我们此时的子数组终点直接从之前的位置开始，若当前子数组满足条件，那么也就找到了以第二个元素为起点的满足条件的子数组，所以接下来再继续移动起点，也即去寻找以第三个元素为起点的满足条件的子数组。重复这个**暴力枚举优化版**直到结束，整个过程就像一个滑动的窗口，故也叫滑动窗口
所以我们采用所谓滑窗，其实也是暴力枚举，只不过做了优化，时间复杂度从O(n*n)到了O(n）.


***


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>










## markdown语法
### 标题编号测试1 { #1}
*斜体*  
**加粗**  
***斜体加粗***。
> 块引用  
>> 嵌套块引用  
>> 嵌套块引用  
>块引用  

1. 有序列表  
3. 有序列表  
7. 有序列表
    1. 有序列表嵌套
    2. 有序列表嵌套  
    列表嵌套段落
        > 嵌套引用
- 无序列表  
- 无序列表  
- 无序列表
- 无序列表
  - 无序列表嵌套
  - 无序列表嵌套

```
代码块
用三个反引号包裹
```
~~~
代码块
用三个波浪号包裹
~~~
```python
# 代码块
# 围栏后接语言类型
import sys
if 1 == 1 :
  print('this is python code block~')
```

脚注[^1]  
脚注[^2]

[链接到测试标题1](#1)

~~双波浪线包裹表示删除线~~

- [x] 任务列表1
- [x] 任务列表2
- [ ] 任务列表3

emoj使用：

:joy:  
自动网址链接：
www.baidu.com

反引号包裹以取消自动网址链接：
`www.baidu.com`  

三个星号单独一行表示分割线：
***

链接  
[链接显示名](https://www.baidu.com "去往百度")  
图片  
![这是图片名称](https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg "图片说明")








[^1]:这是脚注1.
[^2]:这是脚注2.


