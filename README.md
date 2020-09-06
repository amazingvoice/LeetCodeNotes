# LeetCodeNotes

## Array:
### 88. Merge Sorted Array
**描述**：合并两个有序数组，将B合并入A，A长度刚好为A.length + B.length
```
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3
```

**思路**：从后往前将B并入A可以避免使用额外空间

### 189. Rotate Array
**描述**：数组向右旋转k个位置

**思路**：见编程珠玑2.3节

### 922. Sort Array By Parity II
**描述**：给定 **int[] A** , 其中一半奇数一半偶数，对其排序使得 **int[i]** 的奇偶性与 **i** 相同。

**思路**：使用额外存储空间的方法较为简单，主要说in place方法。使用两个游标，**i** 遍历偶数下标，**j** 遍历奇数下标，确保**i** 移动过程中**A[i]** 都为偶数，如果不是，移动**j** 找到**A[j]** 为偶数的位置，对换**A[i]** 与**A[j]** 。

### 121. Best Time to Buy and Sell Stock
**描述**：int[] 存储每日股价，找出买入和卖出日期，使该交易获利最大。

**思路**：遍历数组，出现价格新低时更新minPrice变量，不是新低时，与minPrice求差更新maxProfit变量。O(n)时间

## Hash Table:
### 1. Two Sum
**描述**：从 **int[] nums** 中找出两个数（下标不同），使两数之和等于**m**。

**思路**：使用**HashTable**实现 **O(n)** 时间求解，在遍历数组时往 **HashTable** 里添加项 **(nums[i], i)** ，并同时查找 **m - nums[i]** 是否已存在于哈希表中。

### 219. Contains Duplicate II
**描述**：给定int[] A和int k, 判断数组中是否有两个下标i, j使得A[i] == A[j]且abs(i - j) <= k

**思路**：遍历A过程中，向HashSet中添加A[i], 加入前判断HashSet中有无该元素，若有则返回true，无则插入，同时保证HashSet中元素个数 <= k, 如果个数大于k时，从中删除A[i - k]

### 914. X of a Kind in a Deck of Cards
**描述**：给定int[] A, 判断能否找出一个X >= 2, 使得将A分为m >= 1 组，每组有且仅有X个元素，X个元素值相同

**思路**：将所有元素存在一个HashTable中，key为值，value为该值的个数，然后找所有value的最大公约数g, 如果g >= 2, 则X = g

### 1346. Check If N and Its Double Exist
**描述**：给定int[] A, 判断数组中是否有两个下标i, j(i != j)，使得A[i] == 2 * A[j]

**思路**：遍历数组，先判断2 * A[i] 或 A[i] % 2 == 0时A[i] / 2 是否在HashSet中，如果是，返回true，否的话将A[i]插入HashSet

## Dynamic Programming:
### 746. Min Cost Climbing Stairs
**描述**：int[]数组表示爬每层楼梯的cost，花费cost后可爬升1或2阶，可从第1阶或者第2阶开始爬。求爬到顶的最低花费

**思路**：
正序和倒序两种动态规划方案。  
正序f[i]为爬到第i阶的最小花费，f[i] = min(f[i-1] + cost[i-1], f[i-2] + cost[i-2])  
倒序f[i]为从i阶爬到顶的最小花费，f[i] = cost[i] + min(f[i+1], f[i+2])

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

