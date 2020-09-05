# LeetCodeNotes

下面按tag分类题目：

## Array:
### 1. Two Sum
描述：从 **int[] nums** 中找出两个数（下标不同），使两数之和等于**m**。
思路：使用**HashTable**实现 **O(n)** 时间求解，在遍历数组时往 **HashTable** 里添加项 **(nums[i], i)** ，并同时查找 **m - nums[i]** 是否已存在于哈希表中。
