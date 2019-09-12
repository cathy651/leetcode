# LintCode 141. Sqrt(x)

## 题目

Implement int sqrt(int x).

Compute and return the square root of x.

Example 1:
	Input:  0
	Output: 0


Example 2:
	Input:  3
	Output: 1

	Explanation:
	return the largest integer y that y*y <= x.

Example 3:
	Input:  4
	Output: 2

## 思路ideas

基础二分法。主要还是数学题。这道题就是说找到int a 使得 a*a <= target；

代码如下：

```java
public class Solution {
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    public int sqrt(int x) {
        int start = 0;
        int end = x;

        while(start + 1 < end){
          int mid = start + (end - start)/2;
          if(mid * mid > x){
            end = mid;
          }else{
            start = mid;
          }
        }

        if(end*end <= x){
          return end;
        }else{
          return start;
        }
    }
}
```

## 总结Conclusion

- binary search
- time O(logn), Space O(1);
- 追加：如果我们需要考虑小数怎么办。

例如：

Input:  3
Output: 1.73205

代码如下：

```java
public class Solution {

    public int sqrt(int x) {
        int start = 0;
        int end = x;

        // 提前判断一下，如果x 小于等于一，直接就可以缩小end 的范围。
        if(x <= 1.0){
          end = 1.0;
        }
        while(start < end){
          int mid = start + (end - start)/2;
          if(mid * mid > x){
            end = mid;
          }else{
            start = mid;
          }
        }
          return start;
    }
}

```
