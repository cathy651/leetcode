# Lintcode 618 Search Graph Nodes


## 题目

Given a undirected graph, a node and a target, return the nearest node to given node which value of it is target, return NULL if you can't find.

There is a mapping store the nodes' values in the given parameters.

Notice
It's guaranteed there is only one available solution


Example
2------  3 -    5
 \        |     |
   \      |     |
     \    |     |
       \  |     |
         1 -- 4
Give a node 1, target is 50

there a hash named values which is [3,4,10,50,50], represent:
Value of node 1 is 3
Value of node 2 is 4
Value of node 3 is 10
Value of node 4 is 50
Value of node 5 is 50

Return node 4


## 思路ideas

从当前节点开始BFS。Level order traversal in graph. 比较每一个遍历的点mapping出来的值是不是target。如果是就return。如果不是，把这个点的邻居都加入queue里。注意加的时候用hash 先检测一下要加的点有没有被遍历过。

对于Queue 的题目，一般模版：
- initial a queue 存下一层需要visit 的node
- initial a ?? hash set 存已经visited 的node, 这样可以保证visit 过的元素不会被遍历第二次
- 把root 或者当前node 放到queue 中
- 开始while loop, loop 条件是queue 不为空。 如果有node 满足条件，就返回

代码如下：

```java

public class Solution {
	public static void main(String[] args){
		int[] nums = {4,5,6,1,2,3};
		int target = 6;
		System.out.println(search(nums,target));
	}

	public static int search(int[] nums, int target){
		// corner case
		if(nums == null || nums.length == 0){
			return -1;
		}
		int l = 0;
		int r = nums.length -1;
		int res = 0;

		//loop
		while(l <= r){
			int mid = l + (r - l)/2;
			if(nums[mid] == target){
				res = mid;
				return res;
			}
			// 右边单调递增
			if(nums[mid] <= nums[r]){
				if(nums[mid] < target && target <= nums[r]){
					l = mid + 1;
				}else{
					r = mid - 1;
				}
			}
			//左边单调递增
			if(nums[l] <= nums[mid]){
				if(nums[l] <= target && target < nums[mid]){
					r = mid - 1;
				}else{
					l = mid + 1;
				}
			}
		}
		return -1;
	}
}

```



## 总结Conclusion

- two pointers
- 因为要求时间logn, 所以想到binary search.
- time O(logn), Space O(1);
