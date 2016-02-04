##LeetCode解题报告
####17. Letter Combinations of a Phone Number
#####题目内容：
***
Given a digit string, return all possible letter combinations that the number could represent.

    Input:Digit string "23"
    Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;注意判断输入为空字符串的情况。
#####核心代码：
    class Solution
    {
    public:
        vector<string> letterCombinations(string digits)
        {
            if (!digits.size())
                return {};
            vector<string> result(1, "");
            string phoneMap[] = {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
            for (int i = 0; i < digits.size(); i++)
            {
                vector<string> tmp;
                string str = phoneMap[digits[i] - '0'];
                for (int j = 0; j < result.size(); j++)
                    for (int k = 0; k < str.size(); k++)
                        tmp.push_back(result[j] + str[k]);
                result = tmp;
            }
            return result;
        }
    };