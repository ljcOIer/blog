在这里我会列举几个常用的STL数据结构与文档。
<!-- more -->
## 1.$vector$
[官网文档](https://cplusplus.com/reference/vector/vector/)

可变长数组(动态数组) 
![alt](http://image.ljcoier.repl.co:80/img/1692362035943-pcskk.png)

STL- $vector$ 常用函数：

* | 代码 | 介绍
------- | ------- | ------- 
1 | `v.push_back(int num)` | 从队后插入一个元素 
2 | `v.pop_back()` | 删除最后一个元素
5 | `v.begin()` | 返回数组第一个数的位置（指针）
6 | `v.end()` | 返回数组最后一个数的位置（指针）
5 | `v.empty()` | 返回数组是否为空  
6 | `v.size()` | 返回数组元素的个数  



## 2.$queue$
[官网文档](https://cplusplus.com/reference/queue/queue/)

队列 - 先进先出
![alt](http://image.ljcoier.repl.co:80/img/1692359678271-nnbey.png)

STL- $queue$ 函数：

* | 代码 | 介绍  | 时间复杂度 
------- | ------- | -------  | -------  
1 | `q.push(int num)` | 从队后插入一个元素 | $O(1)$
2 | `q.pop()` | 从前面删除一个元素 | $O(1)$
3 | `q.front()` | 返回队首元素 | $O(1)$
4 | `q.back()` | 返回队尾元素 | $O(1)$
5 | `q.empty()` | 返回队列是否为空  | $O(1)$
6 | `q.size()` | 返回队列元素的个数  | $O(1)$

## 3.priority_queue
[官网文档](https://cplusplus.com/reference/queue/priority_queue/)

优先队列 - 返回最大的一个元素

![alt](http://image.ljcoier.repl.co:80/img/1692361213971-qdkbp.png)

STL-priority_queue

* | 代码 | 介绍  | 时间复杂度 
------- | ------- | -------  | -------  
1 | `pq.push(int num)` | 向队列插入一个元素 | $O(Log_{n})$
2 | `pq.pop()` | 删除队列中最大的元素 |  $O(Log_{n})$
3 | `pq.top()` | 返回队列中最大的元素 | $O(1)$
4 | `pq.empty()` | 返回队列是否为空  |  $O(1)$
5 | `pq.size()` | 返回队列元素的个数  | $O(1)$


## 4.map
[官网文档](https://cplusplus.com/reference/map/map/)

字典 - 用来记录关键字

map包含一个键和值，一般使用键获取值，一般在一些要记录的字符串或者数组太长的时候使用，如果觉得时间复杂度不够可以改成`unordered_map`用法基本一样，但是实现方式不同。

![alt](http://image.ljcoier.repl.co:80/img/1692362994779-chzov.png)

STL-map

* | 代码 | 介绍  
------- | ------- | ------- 
1 | `mp[x]=num` | 修改/添加一个键为x值为num的字典 
2 | `mp[x]` | 获取键为x的值
3 | `mp.count(x)` | 获取键为x的字典是否存在
4 | `mp.empty()` | 返回队列是否为空
5 | `mp.size()` | 返回队列元素的个数
