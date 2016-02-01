##LeetCode解题报告
####13. Roman to Integer
#####题目内容：
***
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;依次枚举罗马数字的每一位，如果当前位比上一位大则减去上一位所代表的数字，否则依次做加法。
#####核心代码：
    class Solution
    {
    public:
        int val(const char x)
        {
            switch (x)
            {
                case 'I': return 1;
                case 'V': return 5;
                case 'X': return 10;
                case 'L': return 50;
                case 'C': return 100;
                case 'D': return 500;
                case 'M': return 1000;
                default:  return 0;
            }
        }

        int romanToInt(string s)
        {
            int ans = val(s[0]), pre = val(s[0]);
            for(int i = 1; i < s.size(); i++)
            {
                int tmp = val(s[i]);
                if (tmp > pre)
                    ans -= pre * 2;
                ans += tmp;
                pre = tmp;
            }
            return ans;
        }
    };