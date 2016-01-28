##LeetCode解题报告
####8. String to Integer (atoi)
#####题目内容：
***
Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Requirements for atoi:
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;和普通的字符串转数字函数相比，题目还要求我们能正确的删去多余的空格，忽略无关的信息，识别无效的格式，并判断是否越界。因此只需多加几个判断条件即可。

#####核心代码：
	class Solution
    {
    public:
        int myAtoi(string str)
        {
            bool negative = false;
            int index = 0;
            long long ans = 0;
            while (str[index] == ' ')   index++;
            if (str[index] == '-')
            {
                negative = true;
                index++;
            }
            else if (str[index] == '+')
                index++;
            while (index < str.length() && str[index] >= '0' && str[index] <= '9')
            {
                ans = ans * 10 + str[index++] - int('0');
                if (ans > (~0U >> 1))
                    break;
            }
            if (negative)
                ans *= -1;
            if (ans > (~0U >> 1))
                ans = (~0U >> 1);
            if (ans < int(1 << 31))
                ans = int(1 << 31);
            return int(ans);
        }
    };

	   
#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;虽然题目已经帮我们列出了所有可能的特殊情况，第一次写还是忽略了`+`。修改后发现数据`9223372036854775809`使long long越界，于是在转换过程中加入判断防止越界。