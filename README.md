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

- python collections.Counter、.most_common(k)、.defaultdict(int)/defaultdict(lambda:-1)


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



## 力扣第2529题
正整数和负整数的最大计数
- 思路：二分查找到非递减数组的最后一个负整数位置和第一个正整数位置，再根据这两个位置分别算出正整数和负整数的个数，返回最大个数
- 辅助函数 lowBound(nums,target)，找到非递减数组nums的第一个大于等于target的数的位置
- 利用辅助函数找最后一个负整数的位置：lastNegIndex = lowBound(nums,0) -1 ,即，第一个大于等于0的数的位置的左边一个数的位置，即为 最后一个负整数的位置
- 利用辅助函数找第一个正整数的位置：firstPosIndex = lowBound(nums,0 + 1) ,即，第一个大于等于1的数的位置  
附lowBound函数代码：  
```python
def lowBound(nums,target):
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return left
```

## 力扣第34题
在排序数组中查找元素的第一个和最后一个位置
- 通过辅助函数lowBound，二分查找寻找第一个和最后一个位置
- 注意 若是排序数组中没有待查找元素target，此时start == len(nums) or nums\[start\] != target
- 注意 若start存在,end必然存在

## 力扣第35题
搜索插入位置
- 二分查找的运用（lowBound变体）。
附示例代码：
```python
def searchInsert(self, nums, target):
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] < target:
            left = mid + 1
        elif nums[mid] > target:
            right = mid - 1
        else:
            return mid
    return left
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
- python bin(n & 0xffffffff) ： 以字符串形式输出n的补码。原理：若n为正数，没什么好说的；若n为负数，计算机是以补码的方式进行运算，则通过按位与1，得到补码对应的十进制数值，再用bin()函数输出其二进制形式，即为补码。（按位与运算后的二进制不考虑符号位了，默认为正数，这一点可见这篇：[python中的按位运算](https://blog.csdn.net/belong_to_you/article/details/108609889)）
- 采用bin()函数转换为二进制的字符串时，加上一个前导零规避边界情况
- 优化：采用位运算，n & (1<<left) 获取left指向位置的0或1
- python 连续赋值： right = left = 0

## 力扣第209题
长度最小的子数组
- python 最大整型：sys.maxsize
- 采用滑窗思路，从左往右滑，右边界向右滑动直到窗口内的 元素和>=target，再右滑左边界直到窗口内的 元素和<target，重复以上步骤到右边界越界，记录每次满足条件的min子数组长度
- 滑窗注意单层循环应控制右边界右滑，若是控制左边界右滑，等于暴力枚举
- 为什么采用滑窗？滑窗是对暴力解法的优化。暴力枚举：两层循环枚举所有满足条件的子数组，也即外层循环控制子数组的起点，内层循环遍历找到以nums\[i\]为起点的满足条件的最小子数组。重点来了：暴力枚举以数组所有元素为起点的满足条件的子数组，子数组的**右边界是递增的**  
举例说明：  
nums=\[1,2,3,4,5\],target=6。暴力枚举时，  
外层第一次循环找到的以第一个元素1为起点的满足条件的长度最小子数组为\[1,2,3\]，  
外层第二次循环找到的以第二个元素2为起点的满足条件的长度最小子数组为\[2,3,4\],  
外层第三次循环找到的以第三个元素3为起点的满足条件的长度最小子数组为\[3,4\],  
外层第四次循环找到的以第四个元素4为起点的满足条件的长度最小子数组为\[4，5\]  
即满足条件的子数组的右边界index是递增的，这样：在第一次滑动右边界到满足条件停下来时，和暴力枚举一样，找到的是以第一个元素为起点的满足条件的子数组；接下来若是暴力枚举，子数组起点应设置为第二个元素，但由于满足条件的子数组的右边界index是**递增**的，所以我们此时的子数组终点直接从之前的位置开始，若当前子数组满足条件，那么也就找到了以第二个元素为起点的满足条件的子数组，所以接下来再继续移动起点，也即去寻找以第三个元素为起点的满足条件的子数组。重复这个**暴力枚举优化版**直到结束，整个过程就像一个滑动的窗口，故也叫滑动窗口。所以我们采用所谓滑窗，其实也是暴力枚举，只不过做了优化，时间复杂度从O(n*n)到了O(n）.

## 力扣第2231题
按奇偶性交换后的最大数字
- python list1.sort() 将list1排序(升序)，会改变list1；sorted(list1)会返回list1排序(升序)后的数组，不改变list1；形参可选reverse=0升序，reverse=1降序，默认为升序
- 数组快速生成：
```python
l = [i for i in list1 if i != 0]
```
- 取一个正整数的所有位数字：
```python
while n != 0:
    item = n%10
    n = n // 10
```
- python中取一个正整数的所有位数字，可以直接int转str
- 如何在一个选择排序框架中同时实现对奇数和偶数的排序？
- 选择排序的另外一种思路？（交换元素）
- tips: 判断同奇偶：(a - b) % 2 == 0


## 力扣第1309题
解码字母到整数映射
- python ord函数和chr函数：ord('a') = 97,chr(97) = 'a'

## 力扣第1576题
替换所有的问号
- python处理字符串一个比较合适的方式：sList = list(s)......''.join(sList),因为python中的字符串，只允许索引查询，不允许索引更改，比如print(s\[0\])是可行的，但是s\[0\]='a'这种尝试通过索引方式改变元素值，不行。
- 如果不转换为list，以上操作可以用s.replace(oldStr,newStr,1)代替.


## 力扣第137题
只出现一次的数字 II
- java 取某数的二进制第i位(从低位到高位编号)：(n>>i) & 1
- java 将某数的二进制第i位置1：n \| (1<<i)

## 力扣第1854题
人口最多的年份
- 差分数组： 第i个元素记录第i年的人口增量(负数表示人口减少)，那么第i年的人口总数就等于从0到i这个闭区间所有的人口增量之和。
- 差分数组求最后一年的人口总数需要遍历整个差分数组，这个过程中，累加到当前第i年时，恰为第i年的人口总数，也即：要遍历所有年份的人口总数，只需要遍历一次差分数组。  


## 力扣第2559题  
统计范围内的元音字符串数
- 概念 数组前缀和：原数组d和其前缀和数组s,则s\[i\] 表示数组d从第0个元素到第i-1个元素的和，通常s的长度为d的长度+1，前缀和常用来解决连续子数组和的问题
- 通过前缀和实现O(1)时间复杂度求连续子数组\[i,j\的和：sum = s\[j+1\] - s\[i\]
- 步骤：1.遍历原数组d，构建前缀和数组；2.通过前缀和求连续子数组的和
- tips：前缀和数组与差分数组刚好是互逆的两种思想  


## 力扣第560题
和为 K 的子数组
- 思路：前缀和+哈希
- 注意**公式的转换**
- 注意prefix数组长度为len(d) + 1


## 力扣第523题
连续的子数组和
- 思路一样为：前缀和+哈希
- 特别注意：**公式的转换**，同余定理：若(a-b)%k == 0 当且仅当 a%k == b%k ==0。利用同余定理，将公式转换为求同余的前缀和。
- 注意处理子数组长度大于2这一条件
- python collections.defaultdict(lambda:-1)，用来将默认数组的默认value置为-1(你想要置为的值)
示例代码：
```python
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        l = len(nums)
        prefix = [0] *(l+1)
        sumCurr = 0
        for i in range(l):
            prefix[i] = sumCurr
            sumCurr += nums[i]
        prefix[-1] = sumCurr
        mp = collections.defaultdict(lambda:-1)
        for i in range(l+1):
            n = 0
            remainder = prefix[i] % k
            if mp[remainder] != -1 and i - mp[remainder] >= 2:
                return True
            if mp[remainder] == -1:
                mp[remainder] = i
        return False
```



## 力扣第836题
矩形重叠
- 判断一维线段是否有重叠: (x1,x2),(x3,x4)，那么当且仅当：max(x1,x3) < min(x2,x4)成立，两线段有重叠，也即：两线段**起点的最大值**小于**终点的最小值**时，两线段有重叠
- tips:两线段重叠的重叠率IoU计算公式：IoU = ( min(x2,x4) - max(x1,x3) ) / ( max(x2,x4) - min(x1,x3) )，也即：重叠长度/总长度
- 矩阵重叠则是将以上问题拓展到二维空间，若要两矩阵重叠，则**两矩阵在x轴上的投影和y轴上的投影都要重叠**
- rec1:(x1,y1,x2,y2)、rec2(x3,y3,x4,y4)，表示：（左下角坐标，右上角坐标），那么重叠条件: max(x1,x3) < min(x2,x4) and max(y1,y3) < min(y2,y4)
- 该题的另一解：逆向思维，一矩阵在另一矩阵的上、下、左、右时，两矩阵不重叠


## 力扣第2364题
统计坏数对的数目
- 公式转换：把j-i != num\[j\] - num\[i\] 转换为num\[i\] - i != num\[j\] - j，这样把本来需要**前向寻找**的问题，转换为**当前+哈希**的问题
- 思路转换：逆向思维，坏数对数量 = 所有数对数量 - 好数对数量
- 通过以上两点，问题转化为找好数对及统计其数量，我们用哈希来做
- **特别注意：代码中i、j是有大小顺序的！本题中i、j大小顺序无所谓，但是换个公式的话，i、j大小顺序就很重要了，循环中的循环变量i，应视作公式中i、j的较大者**
- 同类型题[1814. 统计一个数组中好对子的数目](https://leetcode.cn/problems/count-nice-pairs-in-an-array/)  
  
示例代码
```python
class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        mp = collections.Counter()
        cnt = 0
        l = len(nums)
        for i in range(l):
            cnt += mp[nums[i] - i]
            mp[nums[i] - i] += 1
        total = l * (l-1) // 2
        return total - cnt
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


