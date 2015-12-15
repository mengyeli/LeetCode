##LeetCode解题报告
####5. Longest Palindromic Substring
#####题目内容：
***
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;暴力算法为枚举每一个字串，判断是否回文，时间复杂度为O(n^3)。可以通过枚举子串中点的方法优化到O(n^2)，提交到oj上后仍然超时。
***

* Manacher算法，明天完成。

***
#####核心代码：
	