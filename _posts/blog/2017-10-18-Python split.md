---
layout: post
title: Python 分割器和无限迭代器
category: blog
---
```
from itertools import cycle
s="""1,2,3,4,5,6,7,8,9,10"""
a=[]
for i in s.split(','):
	i="<span style=\"font-size:0px; line-height:normal;\">"+i+"</span>"
	a.append(i)
# for x in a:
# 	print(x)
d=cycle("很高兴")
e=zip(a,d)
for i,g in e:
	print(i,g)
```
结果：
```
<span style="font-size:0px; line-height:normal;">1</span> 很
<span style="font-size:0px; line-height:normal;">2</span> 高
<span style="font-size:0px; line-height:normal;">3</span> 兴
<span style="font-size:0px; line-height:normal;">4</span> 很
<span style="font-size:0px; line-height:normal;">5</span> 高
<span style="font-size:0px; line-height:normal;">6</span> 兴
<span style="font-size:0px; line-height:normal;">7</span> 很
<span style="font-size:0px; line-height:normal;">8</span> 高
<span style="font-size:0px; line-height:normal;">9</span> 兴
<span style="font-size:0px; line-height:normal;">10</span> 很
```
上面的列子大概是要这样的效果：

list=[1,2,3,4,5,6]
l=[a,b,c]
结果为：
1a,2b,3c,
4a,5b,6c


如果要这样呢
l=[1,2,3,4,5,6,7,8,9,10,11,12]
k=[a,b,c]
结果为：
1a2,3b4,5c6,
7a8,9b10,11c12
那就
```
from itertools import cycle
 
s="""1,2,3,4,5,6,7,8,9,10,11,12"""
a=[]
for i in s.split(','):
	i="<span style=\"font-size:0px; line-height:normal;\">"+i+"</span>"
	a.append(i)

d=cycle('很高兴')
e=zip(a[::2],d,a[1::2])
for q,w,e in e:
	print(q,w,e)
```
结果：
```
<span style="font-size:0px; line-height:normal;">1</span> 很 <span style="font-size:0px; line-height:normal;">2</span>
<span style="font-size:0px; line-height:normal;">3</span> 高 <span style="font-size:0px; line-height:normal;">4</span>
<span style="font-size:0px; line-height:normal;">5</span> 兴 <span style="font-size:0px; line-height:normal;">6</span>

<span style="font-size:0px; line-height:normal;">7</span> 很 <span style="font-size:0px; line-height:normal;">8</span>
<span style="font-size:0px; line-height:normal;">9</span> 高 <span style="font-size:0px; line-height:normal;">10</span>
<span style="font-size:0px; line-height:normal;">11</span> 兴 <span style="font-size:0px; line-height:normal;">12</span>
```
是不是很无聊？