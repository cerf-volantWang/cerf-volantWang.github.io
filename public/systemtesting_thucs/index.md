# 计算机系统性能测试


这门课程由贵系的翟季冬老师于2023年秋季开设。

## 计算机性能测试与分析



## 平均值的选取



## 静态性能分析




## 测量误差
Lecturer: 翟季冬

误差的定义：测量结果偏离真实值的程度。
- 测试值 = 真实值 + 误差

误差 in System
- interruption and system service
- multi-thread
- ...

### 例子
测试硬盘带宽
```c++
for(size = 1; size<32G;){
  fd = open(new_file);
  t1 = start_time;
  for(int i=0; i<count; i++){
    write(fd,buf,size);
  }
  t2 = stop_time;
  total_size = count * size;
  bandwidth = total_size / (t2 - t1);
  close(fd);
  size = size * 2;
}
```
测的只是内存带宽！OS有buffer cache.
文件系统缓存带来的影响，`fsync()`



### 系统误差和随机误差



系统误差
- I/O写性能
- 测试的错误，尽可能避免

随机误差
- unpredictable
- unbiased



### 误差模型

伯努利玻璃珠？二项分布 $\Rightarrow$ 高斯分布

- Precision
- Accuracy

量化误差——用置信区间量化测试精度

画折线图抖动很大





《量化研究方法》很多假设正态分布

+ 但很多不符合正态分布！Statistical performance comparisons of computers, Tianshi Chen and Yunji Chen, HPCA 2012
+ textbooks/papers perhaps not right!
  + results may not be correct
  + but methodology is important
+ key-value storage: Amazon's may differ from each other
  + different situations



作业（考研题）

自己写程序测量你的计算机上

+ 内存到CPU的**带宽**
+ Cache到CPU的**带宽**
  + Cache用户透明
  + 数据Cache和指令Cache

读带宽/写带宽？

论文原始题目是：

Cache是几路/多大 L1/L2/L3多大？替换策略？都可以写程序测出来！

某年sigmetrics，pingkali?cornell->ut austin



## 计算机系统的复杂性



系统的复杂性到底来自哪些方面？

做系统的难点体现在哪里？

### What is a System?

+ System
  + interacting set of components with a specified behavior at the interface with its environment
+ Examples
  + web, android, linux



+ Hard to define; but has some symptoms:
  + large number of components $\Rightarrow$ 大规模分布式系统
  + large number of connections $\Rightarrow$ 互联网
  + Irregular $\Rightarrow$ 稀疏、图计算问题
  + No short description
  + Many people required to design/maintain



System papers:

+ no difficult math formulas
+ we have solved a very difficult problem



Problem Types

+ Emergent properties
+ Propagation of effects
+ Incommensurate scaling
+ Trade-offs

#### Emergent Proterties

Features

+ no evident in the individual components of a system
+ but show up when combining those components
+ might also be called surprises
+ an unalterable fact

Example

The Millennium Bridge



#### Propagation of Effects

solution to a certain problem may cause a series of problems!



#### Incommensurate Scaling



#### Trade-offs

系统吞吐 vs 用户等待时间



> We find that we were born too soon.

in place of a well-organized theory, we use case studies



+ Modularity
+ Abstraction
+ Layering
+ Hierarchy
  + DNS System



设计是理想的，现实是骨感的！

> Any problem in computer science can be solved with another level of indirection
>
> performance...reduce a level







1. 95%置信区间
2. 计算机系统的复杂性来自于很多方面，积累非常重要！Do some dirty work!
3. CESM？编译？
4. 不是记住多少东西，而是掌握思考的逻辑




