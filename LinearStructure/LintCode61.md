# 61. Search for a Range



## 题目

Given a sorted array of n integers, find the starting and ending position of a given target value.

If the target is not found in the array, return [-1, -1]

Example 1:

Input:
[]
9
Output:
[-1,-1]

Example 2:

Input:
[5, 7, 7, 8, 8, 10]
8
Output:
[3, 4]

Challenge
O(log n) time.

## 思路ideas

暴力解法就是从左到右遍历整个数组，找到target 之后开始记录，一直到没有target的位置。时间O(n).

题目要求O(log n) 很明显要用binary search. 这道题无非就是把之前二分法的找第一次模版用两遍。

我们复习下二分法的模版

```java


        // 至少有三个数的时候
        int start = 0;
        int end = nums.length -1;
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            // 求第一个数字的位置
            if(nums[mid] >= target){
                end = mid;
            }else{
                start = mid;
            }
        }

        if(nums[start] == target){
          return start;
        }else if{
          if(nums[end] == target) return end;
        } else{
          return -1;
        }



```

代码如下：？？？ 在console 里面说return ; 是illegal start of expression

```java
public class Solution {
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchRange(int[] A, int target) {
        if(A.length == 0 || A == null) return [-1,-1];

        int lRes = 0;
        int rRes = 0;
        // 找第一次出现
        int start1 = 0;
        int end1 = A.length -1;
        while(start1 + 1 < end1){
          int mid = start1 + (end1 - start1)/2;
          if(A[mid] >= target){
            end1 = mid;
          }else{
            start1 = mid;
          }
        }

        if(A[start1] == target){
          lRes = start1;
        }else if(A[end1] == target){
          lRes = end1;
        }else{
          return [-1,-1];
        }

        // 找最后一次出现
        int start2 = lRes;
        int end2 = A.length -1;
        while(start2 + 1 < end2){
          int mid = start2 + (end2 - start2)/2;
          if(A[mid] <= target){
            start2 = mid;
          }else{
            end2 = mid;
          }
        }

        if(A[end2] == target){
          rRes = end2;
        }else{
          rRes = lRes;
        }

        // return res
        return [lRes, rRes];
    }
}

```


## 总结Conclusion

- two pointers,binary search
- time O(logn) time, Space O(1);
