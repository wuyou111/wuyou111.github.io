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
左闭右闭
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
左闭右开
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


