# LintCode 14. First Position of Target


## 题目

For a given sorted array (ascending order) and a target number, find the first index of this number in O(log n) time complexity.

If the target number does not exist in the array, return -1.

## 思路ideas

最简单的二分法，两头到中间。
有一个地方需要注意：因为目标是target第一次出现的位置，所以缩小范围的时候如果是end = target 也不一定符合要求。



代码如下：

```java

public class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        // write your code here
        if(nums == null || nums.length == 0) return -1;

        int start = 0;
        int end = nums.length -1;

        // 至少有三个数的时候
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            // 求第一个数字的位置
            if(nums[mid] >= target){
                end = mid;
            }else{
                start = mid;
            }

        }

        if(nums[start] == target) return start;
        if(nums[end] == target) return end;
        return -1;
    }
}


```


## 总结Conclusion

- two pointers
- time O(logn), Space O(1);
