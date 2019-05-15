# Quick sort



## 题目

实现quick sort,

2，3，5，9，4，1，6

定下pivot: 从数列中挑出一个元素，称为”基准”（pivot）。我们这里把最后一个数当作pivot.

分区（partition）操作: 所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面,在这个分区结束之后，该基准就处于数列的中间位置。

Iteration: 把小于基准值元素的子数列和大于基准值元素的子数列排序。递归到最底部时，数列的大小是零或一，也就是已经排序好了。这个算法一定会结束，因为在每次的迭代（iteration）中，它至少会把一个元素摆到它最后的位置去。



## 思路ideas

实现这个sort, 最主要就是写好partition, 利用swap 函数实现套用。


```java

代码如下：

import java.util.*;
// test case
public class QuickSort {
	public static void main(String[] args) {
		int[] arr = new int[]{1,3,5,7,2,4,6,8,4};
		System.out.println(Arrays.toString(quickSort(arr)));
	};

  // start function
  public static int[] quickSort(int[] arr) {
        sort(arr, 0, arr.length - 1);
        return arr;
    }
// method function sort
  public static void sort(int[] arr, int l, int r) {
		if(l > r) return;
		int m = partition(arr, l, r);
		sort(arr, l, m - 1);
		sort(arr, m + 1, r);
	}

// method function partition
	public static int partition(int[] arr, int l, int r) {
		int pivot = arr[r];
		int pos = 0;
		for(int i = l; i < r; i++) {
			if(arr[i] <= pivot) {
				swap(arr, i, pos);
				pos++;
// swap(arr, i, pos++);
			}
		}
		swap(arr, pos, r);
		return pos;
	}

  // helper function swap
	public static void swap(int[] arr, int m, int n) {
		int tmp = arr[m];
		arr[m] = arr[n];
		arr[n] = tmp;
	}
}


```



## 总结Conclusion

- two pointer swap, recursion
- time: O(n^2); space: O(n)
