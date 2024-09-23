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
  
### 数据类型  
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
  
### 常见算法策略  
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

### Array List 顺序表（数组）

- Elements are stored contiguously in memory as an array (easy to find kth element) 元素作为数组连续存储在内存中（容易找到第k个元素）

- Simple array implementation 简单的阵列实现
  
  - Must know estimate of size before hand (waste of space) 必须事先知道尺寸估计（浪费空间）
  
  - Insert and Delete: expensive  插入和删除：昂贵

| 0            |               |
| ------------:|:-------------:|
| 1            | element[1]    |
| 2            | element[2]    |
| 3            | Element[3]    |
|              | ……            |
| 1 ≤ i ≤ last | element[i]    |
|              | ……            |
|              | ……            |
| last         | element[last] |
|              | ……            |
| maxlength-1  |               |

```c
//Type Definition： 类型定义
# define maxlength 100 
struct LIST {      
    elementtype * elements;
    int last; 
}; 
//Position Type：重定义
    typedef int position; 
//Linear List L: 声明结构
    struct LIST L; 
//Initialization: 初始化
    L.elements= (elemttype *)  malloc  (maxlength* sizeof (elemttype))  
//Representation：调用
    L.elements[p] // pth element       
    L.last // length of L, position of last element 
```

#### 插入（前插） Array list-INSERT Operation

```c
 void Insert (int newItem, List &L, int location) {       
     int i;       
     if (L.last + 1 == maxlength) {//array is full 数组已满          
         int *b = new int[2 * maxlength]; // Allocate a new array, twice as long. 分配一个新数组，长度是原来的两倍。
         for (i = 0; i <= L.last; i++) {// Copy items to the bigger array.将项目复制到更大的数组。
             b[i] = L.elements[i];           
         }       
         L.elements = b; // Replace the too-small array with the new one.用新的阵列替换太小的阵列。
     }       
     for (i = L.last; i >= location; i--) { // Shift items to the right.将项目向右移动。
         L.elements[i + 1] = L.elements[i];       
     }      
     L.elements[location] = newItem;      
     L.last++; 
 }//Time Complexity 时间复杂度：O(n) 
```

#### 删除 Array list-DELETE Operation

```c
 void Delete( Element X, LIST &L) {   
     position i, q ;     
     for (  i= 0 ; i <= L.last ; i ++ ){          
         if ( L.elements[ i ] == X ){    
             q = i;//find the position of X          
             break;          
         }     
     }     
     if ( i == L.last+1)// X found or not?
        error (not found X)；     
     else{             
         L.last = L.last – 1;          
         for ( i = q ; i < L.last ; i ++ ){        
             L.elements[ i ] = L.elements[ i + 1 ]; //move all elements       
         } 
     }//Time Complexity：O(n) 
```
