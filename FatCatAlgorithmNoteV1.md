# 【1】Array and Linked List

## Array

### If the problem allows you to alter the content of the array

#### [Searching Repeated Elements]

**Description**

There is an array with a length of N whose elements are integer within the limits of [0, n-1]. Some of the elements in the array is not unique, but we have no idea on either which elements are they, nor how many times the elements repeated. Please find any one of the repeated elements.

**Constrains**

time complexity : $O(N)$

space complexity : $O(1)$

**E.g.**

【Input】

```
{2, 3, 1, 0, 2}
```

【Output】

```bash
2
```

 

。

。

。

。

。



**Insight**

Since this is the first problem of this note, here is a recommed framework of analysing problems from the same level (Namely, a very novel level only for some good, not awesome companies's  interview)

First : *Learn the basic information of the problem*

such as the legality(合法性) of some operations (e.g., could we change the content of this array or not ) ; 

Second : *Limitation (边界)*

for this problem, we should make sure $N \ge 1$

Finally : *Find some latent conditions to support our solution*

for this problem, we want to alter some elements to solve the problem, and the latent condition is that, we can alter.



。

。

。



**Solution**

We use Linear Probing(线性探查法) to solve this problem.

If we move the elements of the array, finally an array without repeated element will be subject to a mapping: number[i] == i ; but if there is repeated array, then there will have mismatch;

the var i denotes the index of our checking, and i will go through the array from 0 to N-1;

if numbers[i] == i, then i++;

if numbers[i] != i, we fetch the numbers[i] and move it to where it should be : the index (numbers[i]); if the object index still mismatch, then we can repeat this step until we find something match; if the object index is already matched, then the fetched element is what we want.



```c++
class Solution:{
    public:
    int findRepeat(vector<int>& numbers){
        if(numbers.size() == 0)return -1;
        
        for(int i=0; i<numbers.size(); ++i){
            if(numbers[i] == i)continue;
            
            int tmp = numbers[i];
            do{
                if(number[tmp] == tmp)return tmp;
                swap(tmp, numbers[tmp]);  //善用辅助函数
            }while(numbers[i] != i);  //注意这个分号
            
        }
        
        return -1;
        
    }
}
```



### Searching Array

#### [Searching in an 2D Array]

**Description**

Given a 2D M*N array, and all value from top to down are increase, and all value from left to right are increase, too. If there is an integer X, please search if X exits in the given array.

 **Constrains**

$0 \le M, N, \le 50$

$0 \le X \le 10^9$

time complexity : $O(M + N)$

space complexity : $O(1)$

**E.g.**

【Input】

```bash
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
], 5
```

【Output】

```
True
```



。

。

。

。

。



**Insight**

Because of the speciality of this problem condition, we can use a solution similar to "binary search".

The common solution of a searching problem is DFS. However, for this problem, we can choose another way.



。

。

。



**Solution**

We start searching at the right-up corner(or left-down corner), other place may cause layers of recursion.

```java
public boolean Find(int target, int[][] matrix) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
        return false;
    int rows = matrix.length, cols = matrix[0].length;
    int r = 0, c = cols - 1; // 从右上角开始
    while (r <= rows - 1 && c >= 0) {
        if (target == matrix[r][c])
            return true;
        else if (target > matrix[r][c])
            r++;
        else
            c--;
    }
    return false;
}
```



