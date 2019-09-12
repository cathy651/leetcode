# 617. Maximum Average Subarray II

## 题目

Given an array with positive and negative numbers, find the maximum average subarray which length should be greater or equal to given length k.
​​
Example 1:

Input:

[1,12,-5,-6,50,3]

3

Output:

15.667

Explanation:

 (-6 + 50 + 3) / 3 = 15.667

Example 2:

Input:

[5]

1

Output:

5.000

## 思路ideas

二分法，首先基础的两边到中间，找target 是否存在在数组，如果存在，那么直接把target 放进去，然后比较target左右两边把更相近的放进去。

如果target 不存在, 那么return 什么？

```java
if(nums[start] == target) return start;
if(nums[end] == target) return end;
return ？？？;
```

return start , end 中更接近target 的那个的位置.我们可以简化上面的变成两行，

```java
if(target - A[start] <= A[end] - target){
     return left;
}else{
    return right;
}
```

为什么视频中return 最后一位数的位置????



代码如下：这个代码run 的时候报错 哪里错了？？？

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

- two pointers,binary search
- time O(logn + k) time, Space O(K);
