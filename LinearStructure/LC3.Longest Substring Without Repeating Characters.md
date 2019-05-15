# LeetCode3. Longest Substring Without Repeating Characters

https://leetcode.com/problems/longest-substring-without-repeating-characters/


## 题目

Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"

Output: 3

Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: "bbbbb"

Output: 1

Explanation: The answer is "b", with the length of 1.

Example 3:

Input: "pwwkew"

Output: 3

Explanation: The answer is "wke", with the length of 3.

Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

代码如下：

```java

class Solution {
    public int lengthOfLongestSubstring(String s) {
        // initial
        int i = 0, j = 0, maxLength = 0;
        Set<Character> set = new HashSet<>();
        // ij 两个指针，j 开始扫描，
        //while(i < s.length() && j < s.length()){ 双指针在后面会规定左边不超过右边，所以一开始就定义右边
        while(j < s.length()){
            if(!set.contains(s.charAt(j))){
                // 如果set 里面没有j 就把j 放入set,然后继续往后扫描j, 同时更新目标长度
                set.add(s.charAt(j));
                j++;
                maxLength = Math.max(maxLength, j - i);
            }else{
                //遇到重复，先删除当前的i 所在元素（因为你要找的是连续不重复，所以重复元素之前的都必须删除）
                set.remove(s.charAt(i));
                i++;
            }
        }
        return maxLength;
    }
}

// 这道题目如果要输出longest substring，
for (String str : set) {  
      System.out.println(str);  
 }  
// Java里面没有连续小于： a < b <= 102 是不对的。需要写成 a < 102 && b < 102, a <=b
// 这个题目主要是指针，hashset；
// 关键在于
// 不重复的时候，一直更新保存结果。
// 如果出现重复，如何删除重复和其之前的所有内容。 例如abcrbde. 在找到第二个b 的时候意味着要删除第一个b 和他之前的所有元素。

```
