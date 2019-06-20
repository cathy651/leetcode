# 460. Find K Closest Elements



## 题目

Given target, a non-negative integer k and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.

The value k is a non-negative integer and will always be smaller than the length of the sorted array.

Length of the given array is positive and will not exceed 10^4
​​
Absolute value of elements in the array will not exceed 10^4
​​

## 思路ideas

二分法，首先基础的两边到中间，找target 是否存在在数组，如果存在，那么直接把target 放进去，然后比较target左右两边把更相近的放进去。

如果target 不存在, 那么return 什么？

```java
if(nums[start] == target) return start;
if(nums[end] == target) return end;
return ？？？;
```

return start , end 中更接近target 的那个的位置

为什么视频中return 最后一位数的位置????



代码如下：这个代码哪里错了？？？

```java

public class Solution {
    /**
     * @param A: an integer array
     * @param target: An integer
     * @param k: An integer
     * @return: an integer array
     */
    public int[] kClosestNumbers(int[] A, int target, int k) {
        // 定义了一个长度是k 的数组
        int[] res = new int[k];

        if(A.length == 0 || A == null) return res;

        firstClosest(A, target, k);
        left = index - 1;
        right = index + 1;
        res[0] = A[index];

        for(int i = 1; i < k; i++){
            if(left < 0){
                res[i] = A[right];
                right++;
            }else if(right > 0){
                res[i] = A[left];
                left--;
            }else{
                if(target - A[left] <= A[right] - target){
                    res[i] = A[left];
                    left--;;
                }else{
                    res[i] = A[right];
                    right++;
                }
            }
        }

        return res;

        private static int firstClosest(int[] A, int target, int k){
            int start = 0;
            int end = A.length -1;

            while(start + 1 < end){
                mid = start + (end - start)/2;
                if(A[mid] >= target){
                    end = mid;
                }else{
                    start = mid;
                }
            }

            if(target - A[start] <= A[end] - target){
                 return left;
            }else{
                return right;
            }
        }
    }
}

```


## 总结Conclusion

- two pointers
- time O(logn + k) time, Space O(K);
