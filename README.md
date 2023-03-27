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


