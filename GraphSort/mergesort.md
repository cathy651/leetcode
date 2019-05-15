# NA merge sort 的实现



## 题目
实现一个merge sort

[intro](http://sunshineyg888.github.io/2016/04/04/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F%20(Merge%20Sort))

归并排序是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。

1）用recursion递归实现：

top-down, 3 = 1+2 ; 1 = 0+1, 你是先找三，然后追溯到1 ，2， 最后追溯到0， 1；

    3

 1      2
 
0 1  

也叫二路归并，先把待排序区间[s,t]以中点二分，接着把左边子区间排序，再把右边子区间排序，最后把左区间和右区间用一次归并操作合并成有序的区间[s,t]。

time : o（log n ）
space: o(n)

```java

import java.util.*;
    // test case
    public class Solution {
    	public static void main(String[] args) {
    		int[] arr = new int[]{1,3,5,7,2,4,6,8};
    		System.out.println(Arrays.toString(mergeSort(arr)));
    	};

      // 主函数
    	public static int[] mergeSort(int[] arr) {
            return sort(arr, 0, arr.length - 1);
        }
        // sort 函数 arr1 is sorted, arr2 is sorted
    	public static int[] sort(int[] arr, int l, int r) {
    		if(l == r) return new int[]{arr[l]};

    		int m = l + (r - l) / 2;
    		int[] leftRes = sort(arr, l, m);
    		int[] rightRes = sort(arr, m + 1, r);
    		return merge(leftRes, rightRes);
    	}

    	// merge 函数
    	public static int[] merge(int[] arr1, int[] arr2) {
    		// corner case

    		// initials
    		int len1 = arr1.length;
    		int len2 = arr2.length;
    		int newLen = len1 + len2;
    		int[] res = new int[newLen];
    		int p = 0;
    		int p1 = 0;
    		int p2 = 0;

    		// for loop
    		while(p1 < len1 && p2 < len2) {
    			if(arr1[p1] <= arr2[p2]) {
    				res[p] = arr1[p1];
    				p++;
    				p1++;
    			} else {
    				res[p] = arr2[p2];
    				p++;
    				p2++;
    			}
    		}
    // 如果出现P1 多出来一个数， p2 已经没有数
    		while(p1 < len1) {
    			res[p] = arr1[p1];
    			p++;
    			p1++;
    		}
    // 如果出现P2 多出来一个数，p1 已经没有数
    		while(p2 < len2) {
    			res[p] = arr2[p2];
    			p++;
    			p2++;
    		}
    		return res;
    	}
    }

```

（2）用iteration迭代实现：
bottom-up

1 个元素的表总是有序的。所以将有n个元素的数组分成 n 个拥有 1 个元素的有序子序列。对子序列两两合并可得 n/2 个子序列，所得子序列除最后一个子序列长度可能为1 外，其余子表长度均为2。再进行两两合并，直到最后得到一个拥有n个元素的有序序列
