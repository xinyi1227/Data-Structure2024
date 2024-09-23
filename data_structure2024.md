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
$$
T_{avg}(N) \And T_{worst}(N)
$$

1. 指令按顺序执行。  
2. 每一步被视作一个时间复杂度。  
3. 整型数据内存大小一定，且拥有无限内存空间。  

#### Asymptotic Notations（渐进表示法） 
$$
T(N)= O(f(N))
$$

![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/cb2f14db6d0200f2e0602e76553274e6c14b6ac3b25b5034243a69084014e7f2.png)

#### 常见时间复杂度  
##### Constant order 常数阶

```c
int sum = 0, n = 100;    // 1 step
sum =  (1 + n ) * n/2;    // 1 step (or 4 step ✓) 
printf (“%d”, sum) ;     // 1 step  
```
$$
T_N   = O(3) = O(1) 
$$ 

##### Linear order 线性阶

```c
int i; for (i = 0; i < n; i++) 
{ 
    /*execution steps of O(1) */ 
} 
```

$$
T_N   = O(N)  
$$

##### Log order 对数阶

```c
int count = 1;
 while (count < n) {
    count = count * 2;      
    /*execution steps of O(1) */ 
} 
```

$$
2^X=n \ge x=log_2n
$$

$$
T_N = O(logn)
$$ 

##### Square order 平方阶

- 1
  
  ```c
  int i j;
  for (i = 0; i < n; i++){      
      for (j = 0; j < n; j++){           
          /*execution steps of O(1) */       
      } 
  } 
  ```
  
$$
T_N   = O(N^2)
$$

- 2
  
  ```c
  int i j;
  for (i = 0; i < m; i++) {
        for (j = 0; j < n; j++){
            /*execution steps of O(1) */       
      } 
  }
    ```
  
$$
T_N   = O(m \times n)
$$

- 3
  
  ```c
  int i j;
  for (i = 0; i < n; i++){
      for (j = i; j < n; j++){
          /*execution steps of O(1) */   
      }
  } 
  ```

$$
T(N) = n + (n-1) + (n-2) +…+1= (n^2+n)/2 = O(n^2)
$$

##### 如何得到O(n)  
- **O(n)的计算**：通常关注算法中最高次项，忽略低次项和常数项。 
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/ccfc33a5f5f2e56e72fdcfef3fd631edee2e99b8713529c5b613c2719d2bfdd9.png) 
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/dd94357049bfd7b751a797a2a7f723d90c47a5945ed40797dd1fe21f736d0496.png)


- 在选择语句中
![](https://github.com/xinyi1227/Data-Structure2024/blob/main/image/7432ccb2a5ab822fed7c91527e83affd8d70e56055f05e2bdae1cd35fc7eab5e.png)

$$
T_{1}(N)+T_{2}(N)= max(O(f(N)),O(g(N)))
$$

$$
T_{1}(N)*T_{2}(N)=O(f(N)*g(N))
$$
  

##### 其他三种（了解即可）  
- Ω(n), θ(n), o(n)  
  
### 常见算法策略  
#### 递归：函数直接或间接调用自身。  
```c
int factorial (int n)
{
    if (n<=1)
        return 1; // one for the base case
    else // one for else
        return n*factorial(n-1); // 1 for multiplication+ 1 for substraction+ cost of evaluation of factorial(n-1)  
}
```
- **斐波那契问题**：Fib(0) = Fib(1) = 1,  Fib(n) = Fib(n-1) + Fib(n-2)
```c
Fib (int N)
{
    if (N<=1)
        return 1;
    else
        return Fib(N-1)+Fib(N-2);
}

```

$$
T(N) = T(N-1)+T(N-2)+2 \ge Fib(N)
(3/2)^N \le Fib(N) \le (5/3)^N 可见时间复杂度呈指数型增长
$$

#### 问题引入：最大子序列求和问题 Maximun Subsequence Sum Problem**
- Given (possibly negative) integers A1, A2, …, AN, find the maximum value of $ {\textstyle \sum_{j}^{k=i}}A_k $
算法1
```c
int  MaxSubsequenceSum ( const int A[],  int  N ) { 
    int  ThisSum,  MaxSum,  i,  j,  k; 
    MaxSum = 0;   /* initialize the maximum sum */
       for( i = 0; i < N; i++ ){ /* start from A[ i ] */
           for( j = i; j < N; j++ ) {   /* end at A[ j ] */
               ThisSum = 0; 
               for( k = i; k <= j; k++){
                   ThisSum += A[k];  /* sum from A[ i ] to A[ j ] */
                   if ( ThisSum > MaxSum)  MaxSum = ThisSum;  /* update max sum */
               }
           }  /* end for-j and for-i */
       }
     return  MaxSum; 
} 
```
$$
T(N) = O(N^3)
$$

算法2
```c
int  MaxSubsequenceSum ( const int A[],  int  N ) { 
    int  ThisSum,  MaxSum,  i,  j; 
    MaxSum = 0;   /* initialize the maximum sum */
    for( i = 0; i < N; i++ )  {   /* start from A[ i ] */
           ThisSum = 0; 
           for( j = i; j < N; j++ ) {   /* end at A[ j ] */
                ThisSum += A[ j ];  /* sum from A[ i ] to A[ j ] */
                 if ( ThisSum > MaxSum ) MaxSum = ThisSum;  /* update max sum */
          }  /* end for-j */
      }  /* end for-i */
      return  MaxSum; 
} 
```
$$
T(N) = O(N^3)
$$

**算法3——分治法（Divide and Conquer）**
将一个数组及其子数组不断从中间分为两部分，通过递归比较L&R&LR的子序列和的大小

```c
// arr[l]...arr[r]

int findMax(int l, int r){
    // 初始化左边子数组的和与最大和
    int sumL = 0, maxL = sum[m];
    // 初始化右边子数组的和与最大和
    int sumR = 0, maxR = sum[m+1];
    
    // 从m向l遍历，寻找左边子数组的最大和
    for (int i = m; i >= l; i--){
        sumL += arr[i];
        maxL = max(maxL, sumL);
    }
    
    // 从m+1向r遍历，寻找右边子数组的最大和
    for (int i = m + 1; i <= r; i++){
        sumR += arr[i];
        maxR = max(maxR, sumR);
    }
    return maxL + maxR;
}

int MaxSubsequenceSum ( int l, int r ){
    // 如果范围只包含一个元素，直接返回该元素的值
    if (l == r) return arr[l];
    else{
        // 使用分治法，找到中间点
        int mid = (l + r) / 2;
        
        // 递归计算左边的最大子数组和
        int L = MaxSubsequenceSum(l, mid); // T(N/2)
        
        // 递归计算右边的最大子数组和
        int R = MaxSubsequenceSum(mid + 1, r); // T(N/2)
        
        // 计算跨越中间点的最大子数组和
        int LR = findMax(l, r); // O(N)
        
        // 返回三者中的最大值
        return max(LR, max(L, R));
    }
}
```

$$
T(N)=2T(N/2)+O(N) = O(NlogN) （过程略）
$$

**算法4——On-line Algorithm**：在线算法，处理输入数据时，必须立即产生输出，无法看到全部输入数据。
- 适合动态输入：如果数据是动态到达的（即流式数据），Kadane’s Algorithm 能够在每一步实时更新结果，因此它是一个在线算法的经典例子。
- 在线算法的使用场景：
    - 流式数据处理：Kadane's Algorithm 适合处理动态输入数据，能够在数据不断变化或增加时持续计算最大子序列和。
    - 实时计算问题：当你不能提前知道所有输入数据时，在线算法能随着数据的到来不断更新最优解。

```c
int MaxSubsequenceSum( const int  A[ ],  int  N ) 
{ 
    int  ThisSum, MaxSum, j; 
/* 1*/ 	ThisSum = MaxSum = 0; 
/* 2*/ 	for ( j = 0; j < N; j++ ) { 
/* 3*/ 	      ThisSum += A[ j ]; 
/* 4*/ 	      if  ( ThisSum > MaxSum ) 
/* 5*/ 		MaxSum = ThisSum; 
/* 6*/ 	      else if ( ThisSum < 0 ) // 当和为负的时候，则必定对后面的数产生负作用，使后一个数变小，所以直接置零将后一个数作为新的子序列的开头
/* 7*/ 		ThisSum = 0;
    }  /* end for-j */
/* 8*/ 	return MaxSum; 
} 

```
$$
T(N) = O(N)
$$
  
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

#### Find and Retrieve Operations
```c
 position Find ( elementtype x ,
                                            LIST L )
{   position q ;
    for ( q = 1; q <= L.last ; q++ )
    if ( L.elements[ q ] == x )
        return ( q ) ;
        return ( L.last + 1 );
}
 //Time Complexity O(n)
```
```c
elementtype Retrieve ( position p ,
                                                LIST L )
{  if ( p > L.last )
        error( illegal position) ;
    else
        return ( L.elements[ p ] ) ;
} 

//Time Complexity O(1)

```

### Linked List 链表
```c
Type definition：
struct celltype {
elementtype element ;
struct celltype *next ;
} ; /*Node Type*/
/*List Type */
typedef struct celltype *LIST;
/*Position Type*/
typedef struct celltype * position;

```
#### Find and Retrieve Operations
```c
position Find ( elementtype x, LIST L )
{  position p ;
    p = L->next ; //pass the pointer to first item
    while ( p != NULL && p ->element != X  )
         p = p→next ;
    return p ;
} //Time Complexity：O(n)

```
```c
elementtype Retrieve ( position p , LIST L )
{
    return ( p →element );
} //Time Complexity：O(1)

```
#### INSERT Operation

```c
void Insert ( elementtype x, position p, LIST &L )
{  position q ;
    q = new celltype ;
    q →element = x ;
    q →next = p →next ;
    p →next = q ;
} //Time Complexity O(1)

```
#### DELETE Operation
```c
void Delete (Element X, LIST &L )
{  position P, TmpCell ;
   p = FindPrevious( X, L ) ;  
   if ( !IsLast( P, L ) ) //not the last element
   {
       TmpCell = P->Next;
        P->Next = TmpCell->Next;
        free ( TmpCell ); 
    }
 } //Time Complexity：O(1)
```
