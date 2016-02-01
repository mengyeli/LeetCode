##LeetCode解题报告
####12. Integer to Roman
#####题目内容：
***
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;模仿罗马数字的构造过程，从大到小依次写出即可。
#####核心代码：
    class Solution
    {
    public:
        string intToRoman(int num)
        {
            const int base[] = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
            const string symbol[] = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
            string ans = "";
            for(int i = 0; num; i++)
            {
                int count = num / base[i];
                num -= count * base[i];
                while(count--)
                    ans += symbol[i];
            }
            return ans;
        }
    };