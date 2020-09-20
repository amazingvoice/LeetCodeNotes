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

### 414. Third Maximum Number
**描述**：找出int[] A里第三大的元素，如不存在返回最大元素

**思路**：不用排序不用去重的解法，维护三个变量x1, x2, x3，遍历数组  
如果A[i] > x1, 则x1, x2向后顺移，x1 = A[i]
如果A[i] > x2, 则x2向后顺移，x2 = A[i]
如果A[i] > x3, x3 = A[i]

### 581. Shortest Unsorted Continuous Subarray
**描述**：给定int[] A, 找出最短的连续子数组，使得该数组排序为升序后，整个数组为升序状态

**思路**：  
找出所有(i, j), 0 < i < j < n, 使得A[i] > A[j], 在所有(i, j)中找出最小的i和最大的j分别作为下界和上界，这个范围即所求的最小子数组  
给数组排序，然后与原数组比对，找出左起第一个不同的元素和右起第一个不同的元素，作为下界和上界  
使用stack，正向遍历A，如保持升序，则持续压栈，出现比栈顶元素小的元素时就pop，pop到栈顶元素比当前元素小，记下栈顶元素的index，遍历完后记录下最小index作为下界；再反向遍历A，如保持降序，则持续压栈，原理与正向相似，最后选出上界。同样思路还可以不使用额外空间

### 605. Can Place Flowers
**描述**：给定int[] A和int n, 值只有1和0， 1代表种花，0代表空位置，某位置能种花的前提是，相邻位置不能有花，判断A种能否再种下n支花

**思路**：求出当前情况下最多还能种多少花进去，如果n小于等于该值，则true  
找出连续为0的子数组，能对应出该子数组最多能种多少花，注意边界情况，数组紧贴A的左端或右端

### 665. Non-decreasing Array
**描述**：给定int[] A, 判断能最更改最多一个元素，使得整个数组为非降序排列

**思路**：遍历数组，找下降点，如果有多于一个下降点，返回false；如果只有一个下降点i，判断A[i] = A[i-1] 或者A[i-1] = A[i]是否可行，如果是，返回true，otherwise返回false

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

### 392. Is Subsequence
**描述**：给定字符串s和t，判断s是否为t的子序列

**思路**：
https://leetcode-cn.com/problems/is-subsequence/solution/pan-duan-zi-xu-lie-by-leetcode-solution/
该动态规划适用于多个s对应一个t的情况，可以提升判断效率

## Tree:
### 1302. Deepest Leaves Sum
**描述**：给定一个二叉树，求所有最深叶子节点的和

**思路**：O(n)时间算法，DFS  
深度大于最大深度，更新最大深度，sum置0，
深度等于最大深度，sum += val
深度小于最大深度，忽略

### 687. Longest Univalue Path
**描述**：二叉树中找出一条最长的路径，该路径上所有节点的值相同

**思路**：https://leetcode.com/problems/longest-univalue-path/solution/

## Math:
### 1025. Divisor Game
**描述**：见题目

**思路**：数学归纳法
https://leetcode-cn.com/problems/divisor-game/solution/chu-shu-bo-yi-by-leetcode-solution/

## String:

### 14. Longest Common Prefix
**描述**：

**思路**： 除了垂直扫描，分别用分治法和二分查找的思想求解该问题，是个不错的练习，二分查找的corner case比较难考虑全

### 44. Wildcard Matching
**描述**：

**思路**： 分别用动态规划和贪心算法实现，动态规划偏向暴力解法，用cache减少重复计算，贪心算法较难考虑全所有场景

### 859. Buddy Strings
**描述**：给定两个字符串A, B，判断是否能对换A中的两个字符，使AB相等

**思路**：  
判断AB长度是否相等：  
    如不相等： 失败  
    如相等：  
        AB是否完全相等：  
            如相等：  
                判断是否有重复字符：  
                    如有： 成功  
                    没有： 失败  
            如不完全相等：  
              判断是否只有两个index处AB不同
    
## Linked List:
### 234. Palindrome Linked List
**描述**：

**思路**：  
复制到数组使用双指针  
递归判断  
快慢指针找出中点，翻转后半部分链表

### 160. Intersection of Two Linked Lists
**描述**：

**思路**：
哈希表的方法，先将一个链表里的所有节点地址放入HashSet，再遍历另一个链表，查set中有无相同地址，第一个有相同地址的节点即为交点  
双指针i,j同时遍历A,B，某一个链表遍历结束后，将i指向另一个链表开头，再同时遍历，另一个链表也遍历结束后，将j指向另一个链表开头，这样AB长度差找出来，再同时遍历i,j，必然同时到达交点

### 141. Linked List Cycle
**描述**：

**思路**：  
哈希表的方法
快慢指针，正确性证明

### 21. Merge Two Sorted Lists
**描述**：

**思路**：  
迭代方法，使用preHead节点作为头节点可简化代码  
递归方法，
```
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        else if (l2 == null) {
            return l1;
        }
        else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }

    }
}
```
### 206. Reverse Linked List
**描述**：

**思路**：  
迭代：  
```
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode nextTemp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextTemp;
    }
    return prev;
}
```
递归：  
```
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode p = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return p;
}
```
### 206. Reverse Linked List
**描述**：

**思路**：https://leetcode.com/problems/delete-node-in-a-linked-list/solution/

### 876. Middle of the Linked List
**描述**：

**思路**：  
```
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```
## Bit Manipulation:
### 461. Hamming Distance
**思路**：循环右移x ^ y,判断最低位是否为1
