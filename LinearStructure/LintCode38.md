#  38. Search a 2D Matrix II

## 题目

Write an efficient algorithm that searches for a value in an m x n matrix, return the occurrence of it.

This matrix has the following properties:

Integers in each row are sorted from left to right.

Integers in each column are sorted from up to bottom.

No duplicate integers in each row or column.

Example 1:

Input:

	[[3,4]]

	target=3

Output:1

Example 2:

Input:

    [
      [1, 3, 5, 7],
      [2, 4, 7, 8],
      [3, 5, 9, 10]
    ]
    target = 7

Output:2

Challenge

O(m+n) time and O(1) extra space

## 思路ideas

这个题目和leetcode 240很类似，O(m+n) time 就是从左下角或者右上角开始走。这是典型的二分查找。从中间到两边，所以我们可以从右上角或者左下角开始。以右上角为例子，如果target比当前数字大就一直往下走，如果比当前数字小就一直往左走。

那么可以从左上角或者右下角开始吗？不可以，因为矩阵的排列方式，如果从左上角走，就会出现两个方向都可以走的情况，不是唯一路线，无法解出来。

代码如下：

```java

public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @param target: An integer you want to search in matrix
     * @return: An integer indicate the total occurrence of target in the given matrix
     */
    public int searchMatrix(int[][] matrix, int target) {
			// corner
			if(nums == null || nums.length == 0)return 0;

			// initial 左下角
			int m = matrix.length;
			int n = matrix[0].length;
			int x = m - 1;
			int y = 0;
			int count = 0;

			// loop
			while( x >= 0 && y < n){
				if(matrix[x][y] > target){
					x--;
				}else if(matrix[x][y] < target){
					y++;
				}else{
					count++;
					y++;
					x--;
				}
		}
			// return
			return count;
    }
}

```


## 总结Conclusion

- two pointers, binary search
- time O(m + n ) time, Space O(1);
- leetcode 240
