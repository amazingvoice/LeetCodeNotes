# LeetCodeNotes

## Array:
### 88. Merge Sorted Array
**描述**：合并两个有序数组，将B合并入A，A长度刚好为A.length + B.length
```
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3
```

**思路**：从后往前将B并入A可以避免使用额外空间

### 121. Best Time to Buy and Sell Stock
**描述**：int[] 存储每日股价，找出买入和卖出日期，使该交易获利最大。

**思路**：遍历数组，出现价格新低时更新minPrice变量，不是新低时，与minPrice求差更新maxProfit变量。O(n)时间

### 189. Rotate Array
**描述**：数组向右旋转k个位置

**思路**：见编程珠玑2.3节

### 581. Shortest Unsorted Continuous Subarray
**描述**：给定int[] A, 找出最短的连续子数组，使得该数组排序为升序后，整个数组为升序状态

**思路**：

### 605. Can Place Flowers
**描述**：给定int[] A和int n, 值只有1和0， 1代表种花，0代表空位置，某位置能种花的前提是，相邻位置不能有花，判断A种能否再种下n支花

**思路**：求出当前情况下最多还能种多少花进去，如果n小于等于该值，则true  
找出连续为0的子数组，能对应出该子数组最多能种多少花，注意边界情况，数组紧贴A的左端或右端

### 922. Sort Array By Parity II
**描述**：给定 **int[] A** , 其中一半奇数一半偶数，对其排序使得 **int[i]** 的奇偶性与 **i** 相同。

**思路**：使用额外存储空间的方法较为简单，主要说in place方法。使用两个游标，**i** 遍历偶数下标，**j** 遍历奇数下标，确保**i** 移动过程中**A[i]** 都为偶数，如果不是，移动**j** 找到**A[j]** 为偶数的位置，对换**A[i]** 与**A[j]** 。

### 941. Valid Mountain Array
**描述**：给定一个数组int[] A, 判断A是否满足如下条件
A.length >= 3
There exists some i with 0 < i < A.length - 1 such that:
A[0] < A[1] < ... A[i-1] < A[i]
A[i] > A[i+1] > ... > A[A.length - 1]

**思路**：先上山，找到山峰后，判断山峰是否为首尾元素，如不是，继续下山，如能下山到最后一个元素，则满足

## Hash Table:
### 1. Two Sum
**描述**：从 **int[] nums** 中找出两个数（下标不同），使两数之和等于**m**。

**思路**：使用**HashTable**实现 **O(n)** 时间求解，在遍历数组时往 **HashTable** 里添加项 **(nums[i], i)** ，并同时查找 **m - nums[i]** 是否已存在于哈希表中。

### 219. Contains Duplicate II
**描述**：给定int[] A和int k, 判断数组中是否有两个下标i, j使得A[i] == A[j]且abs(i - j) <= k

**思路**：遍历A过程中，向HashSet中添加A[i], 加入前判断HashSet中有无该元素，若有则返回true，无则插入，同时保证HashSet中元素个数 <= k, 如果个数大于k时，从中删除A[i - k]

### 532. K-diff Pairs in an Array
**描述**：给定数组int[] A, 从中找出两个数a, b， 使得abs(a - b) == k

**思路**：遍历A过程中，向HashSet中添加A[i], 添加前判断A[i] - k或A[i] + k是否在HashSet里，如果在，就找到了

### 914. X of a Kind in a Deck of Cards
**描述**：给定int[] A, 判断能否找出一个X >= 2, 使得将A分为m >= 1 组，每组有且仅有X个元素，X个元素值相同

**思路**：将所有元素存在一个HashTable中，key为值，value为该值的个数，然后找所有value的最大公约数g, 如果g >= 2, 则X = g  
求N个数最大公约数：  
```
for (int i = 0; i < N; ++i)
    if (count[i] > 0) {
        if (g == -1)
            g = count[i];
        else
            g = gcd(g, count[i]);
    }
    return g;
```

### 1346. Check If N and Its Double Exist
**描述**：给定int[] A, 判断数组中是否有两个下标i, j(i != j)，使得A[i] == 2 * A[j]

**思路**：遍历数组，先判断2 * A[i] 或 A[i] % 2 == 0时A[i] / 2 是否在HashSet中，如果是，返回true，否的话将A[i]插入HashSet

## Dynamic Programming:
### 53. Maximum Subarray
**描述**：int[] 中找出具有最大和的连续子数组

**思路**：f[i] 为以下标i结尾的连续子数组的最大和，f[i] = max(f[i-1] + ai, ai)  
非动态规划方法有Kadane's Algorithm, **O(n)** 时间  
```
for x in numbers:
    current_sum = max(0, current_sum + x)
    best_sum = max(best_sum, current_sum)
return best_sum
```

### 746. Min Cost Climbing Stairs
**描述**：int[]数组表示爬每层楼梯的cost，花费cost后可爬升1或2阶，可从第1阶或者第2阶开始爬。求爬到顶的最低花费

**思路**：
正序和倒序两种动态规划方案。  
正序f[i]为爬到第i阶的最小花费，f[i] = min(f[i-1] + cost[i-1], f[i-2] + cost[i-2])  
倒序f[i]为从i阶爬到顶的最小花费，f[i] = cost[i] + min(f[i+1], f[i+2])

