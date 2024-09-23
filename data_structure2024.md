# 基本概念  
  
## 结构  
  
### 数据结构  
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/32528deb12773601c2a8e683106948a9ee84b021098fd4d18f4e9fa66b0dbe0d.png)
  
#### 逻辑结构  
- **Set**：集合，元素之间无特定关系。  
- **Linear**：线性结构，元素之间存在一对一关系。  
- **Tree**：树状结构，元素之间存在一对多关系。  
- **Graphic**：图状结构，元素之间存在多对多关系。  
  
#### 物理结构  
- **Sequential Storage Structure**（顺序存储结构）：元素在内存中连续存储，如数组。  
- **Linked Storage Structure**（链式存储结构）：元素通过指针或引用连接，如链表。  
  
#### 数据类型  
- **实际数据类型**：如整型、浮点型等。  
- **抽象数据类型 (ADTs, Abstract Data Types)**：用户自定义的数据类型，通过操作集合来定义。  
  - **优点**：模块化设计。  
  
## 算法  
  
### 时间复杂度 T(N)  
  
#### 三个假设 
$T_{avg}(N) \And T_{worst}(N)$
1. 指令按顺序执行。  
2. 每一步被视作一个时间复杂度。  
3. 整型数据内存大小一定，且拥有无限内存空间。  
  
#### Asymptotic Notations（渐进表示法） 
$T(N)= O(f(N))$

![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/cb2f14db6d0200f2e0602e76553274e6c14b6ac3b25b5034243a69084014e7f2.png)
  
##### 如何得到O(n)  
- **O(n)的计算**：通常关注算法中最高次项，忽略低次项和常数项。 
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/ccfc33a5f5f2e56e72fdcfef3fd631edee2e99b8713529c5b613c2719d2bfdd9.png) 
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/dd94357049bfd7b751a797a2a7f723d90c47a5945ed40797dd1fe21f736d0496.png)

$T_{1}(N)+T_{2}(N)= max(O(f(N)),O(g(N)))$
- ![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/7432ccb2a5ab822fed7c91527e83affd8d70e56055f05e2bdae1cd35fc7eab5e.png)
$T_{1}(N)*T_{2}(N)=O(f(N)*g(N))$

##### 其他三种（了解即可）  
- Ω(n), θ(n), o(n)  
  
#### 常见算法策略  
- **递归**：函数直接或间接调用自身。  
- **分治法**：将问题分解成若干子问题，解决子问题后合并结果。  
- **On-line Algorithm**：在线算法，处理输入数据时，必须立即产生输出，无法看到全部输入数据。![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/01b569a098587915dd1be9860e4e15e85efae4882abe6ec1f832412ab9be211e.png)  
  
## 线性表 (Linear List)  
  
### 概念  
线性表是元素间存在一对一关系，每个元素（除了最后一个）都有唯一后继者的列表。  
  
### 类别  
  
#### 一般类  
可以在列表中的任意位置插入和删除数据。  
- **数组**  
- **链表**  
- **游标**（通常指遍历线性表的指针或迭代器）  
- **双链表**  
- **环形链表**  
  
#### 限制类  
只可以在列表的末尾插入或删除数据。  
- **堆栈 (Stack)**：Last-In-First-Out（后进先出）。  
- **队列 (Queue)**：First-In-First-Out（先进先出）。