##LeetCode解题报告
####258. Add Digits

#####题目内容：
***
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up:
Could you do it without any loop/recursion in O(1) runtime?

***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;通过找规律发现答案为从1到9的循环数列。
#####核心代码：
	int addDigits(int num) 
    {
        if (!num)
            return 0;
        return (num - 1) % 9 + 1;
    }

#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;开始没有考虑数字0，导致第一次没有AC，以后注意。
