##LeetCode解题报告
####14. Longest Common Prefix
#####题目内容：
***
Write a function to find the longest common prefix string amongst an array of strings.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;逐位比较即可。
#####核心代码：
	class Solution 
    {
    public:
        string longestCommonPrefix(vector<string>& strs) 
        {
            if (strs.empty())
                return "";
            for (int i = 0; i < strs[0].length(); i++)
            {
                for (int j = 0; j < strs.size(); j++)
                {
                    if (strs[j][i] != strs[0][i])
                        return strs[0].substr(0, i);
                }
            }
            return strs[0];
        }
    };