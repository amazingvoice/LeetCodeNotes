# LeetCodeNotes

## Array:
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

## Dynamic Programming:
### 746. Min Cost Climbing Stairs
**描述**：int[]数组表示爬每层楼梯的cost，花费cost后可爬升1或2阶，可从第1阶或者第2阶开始爬。求爬到顶的最低花费

**思路**：
正序和倒序两种动态规划方案。
正序f[i]为爬到第i阶的最小花费，f[i] = min(f[i-1] + cost[i-1], f[i-2] + cost[i-2])
倒序f[i]为从i阶爬到顶的最小花费，f[i] = cost[i] + min(f[i+1], f[i+2])
