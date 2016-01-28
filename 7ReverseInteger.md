##LeetCode解题报告
####7. Reverse Integer
#####题目内容：
***
Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;刚看到这道题觉得用字符串做很简单，只需要reverse字符串，处理一下负号和多余的0就好。考虑到题目要求越界返回0，则需要把字符串转换成数再判断，效率反而更低。于是直接用long long存被反转的数，然后判断越界即可。

#####核心代码：
	class Solution 
    {
    public:
        int reverse(int x) 
        {
            long long ans = 0;
            while (x)
            {
                ans = ans * 10 + x % 10;
                x /= 10;
            }
            if (ans > (~0U >> 1))
                return 0;
            if (ans < int(1 << 31))
                return 0;
            return ans;
        }
    };   
#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;写到MAXINT时，记得以前在大牛代码里看到过用`#define oo (~0ULL >> 1)`定义无穷大，就写了`(~0U >> 1)`，不知道MININT有什么好的表示方法，姑且先用`int(1 << 31)`，等问题收到回复再回来改。