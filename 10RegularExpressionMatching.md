##LeetCode解题报告
####10. Regular Expression Matching
#####题目内容：
***

Implement regular expression matching with support for `'.'` and `'*'`.

    '.' Matches any single character.
    '*' Matches zero or more of the preceding element.

    The matching should cover the entire input string (not partial).

    The function prototype should be:
    bool isMatch(const char *s, const char *p)

    Some examples:
    isMatch("aa","a") → false
    isMatch("aa","aa") → true
    isMatch("aaa","aa") → false
    isMatch("aa", "a*") → true
    isMatch("aa", ".*") → true
    isMatch("ab", ".*") → true
    isMatch("aab", "c*a*b") → true
***

#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;递归算法的思路是先判断下一位是不是`'*'`，如果不是，则判断当前位是否匹配。如果是`'*'`，则分两种情况讨论：一种情况是`'*'`代表0个前面的字符，则直接递归isMatch(s, p + 2)；另一种情况是`'*'`代表大于等于1个字符，可以在判断当前位是否匹配后，递归isMatch(s + 1, p)。最后递归退出条件为有一个字符串为空。由于没有存储任何值，时间复杂度应该很高。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;根据上边的递归思路可以得出动规算法。用布尔数组f[i][j]，代表s字符串的前i位是否匹配p字符串的前j位，分别写出三种情况的转移方程即可。需要特别注意初始条件的赋值。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;此题还可以用python的re.match()函数解决。
#####核心代码：
递归：

    class Solution
    {
    public:
        bool isMatch(string s, string p)
        {
            if (p.empty())
                return s.empty();
            if (p[1] != '*')
                return !s.empty() && (s[0] == p[0] || p[0] == '.') && isMatch(s.substr(1), p.substr(1));
            else
                return isMatch(s, p.substr(2)) || (!s.empty() && (s[0] == p[0] || p[0] == '.') && isMatch(s.substr(1), p));
        }
    };
DP：
    
    class Solution
    {
    public:
        bool isMatch(string s, string p)
        {
            int sSize = (int)s.size(), pSize = (int)p.size();
            vector< vector<bool> > f(sSize + 1, vector<bool>(pSize + 1, false));
            f[0][0] = true;
            f[0][1] = false;
            for (int i = 1; i <= sSize; i++)
                f[i][0] = false;
            for (int i = 2; i <= pSize; i++)
                f[0][i] = p[i - 1] == '*' && f[0][i - 2];
            for (int i = 1; i <= sSize; i++)
            {
                for (int j = 1; j <= pSize; j++)
                {
                    if (p[j - 1] != '*')
                        f[i][j] = (s[i - 1] == p[j - 1] || p[j - 1] == '.') && f[i - 1][j - 1];
                    else
                        f[i][j] = f[i][j - 2] || ((s[i - 1] == p[j - 2] || p[j - 2] == '.') && f[i - 1][j]);
                }
            }
            return f[sSize][pSize];
        }
    };


#####总结：
* 递归函数里尽量不要用函数。
* 多练习动态规划的题，注意初始条件要考虑全面。