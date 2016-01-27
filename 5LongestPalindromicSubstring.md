##LeetCode解题报告
####5. Longest Palindromic Substring
#####题目内容：
***
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;暴力算法为枚举每一个字串，判断是否回文，时间复杂度为O(n^3)。可以通过枚举子串中点的方法优化到O(n^2)，提交到oj上后仍然超时。于是学习Manacher算法，用O(n)的时间就能找出最长回文子串。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Manacher算法的大致思路是，首先通过在所有字符中间插入`#`将原字符串转换成长度为2n + 1的字符串，以便将长度为奇数和偶数的字符串一起考虑。通过记录在之前计算中回文子串延伸的最远位置，利用对称性可以直接得到已匹配过回文子串的长度，从而使得每个位置只进行一次匹配。

#####核心代码：
	class Solution
    {
    public:
        static const int MAX = 3333;
        string init(string s)
        {
            string ss = "@#";
            for (int i = 0; i < s.length(); i++)
            {
                ss += s[i];
                ss += '#';
            }
            ss += '$';
            return ss;
        }
        string longestPalindrome(string s)
        {
            string substr = "";
            int len[MAX], X = 0, Y = -1, maxlength = 0, maxindex = 0;
            memset(len, 0, sizeof(len));
            s = init(s);
            for (int i = 1; i < s.length(); i++)
            {
                if (i <= Y)
                    len[i] = min(len[2 * X - i], Y - i);
                else
                    len[i] = 1;
                while (s[i + len[i]] == s[i - len[i]])  len[i]++;
                if (len[i] + i > Y)
                {
                    Y = len[i] + i;
                    X = i;
                }
                if (len[i] > maxlength)
                {
                    maxlength = len[i];
                    maxindex = i;
                }
            }
            maxlength--;
            for (int i = maxindex - maxlength; i <= maxindex + maxlength; i++)
            {
                if (s[i] != '#')
                    substr += s[i];
            }
            return substr;
        }
    };