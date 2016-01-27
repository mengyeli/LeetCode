##LeetCode解题报告
####6. ZigZag Conversion
#####题目内容：
***
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

    P   A   H   N
    A P L S I I G
    Y   I   R
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:

    `string convert(string text, int nRows);
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;看到这类题，一种想法是创建一个字符串数组模拟转换过程，另一种想法是寻找数学规律。直接模拟最简便。

#####核心代码：
	class Solution
    {
    public:
        string convert(string s, int numRows)
        {
            if (numRows <= 1)
                return s;
            string *str = new string[numRows];
            int row = 0, flag = 1;
            for (int i = 0; i < s.length(); i++)
            {
                str[row] += s[i];
                if (row == 0)
                    flag = 1;
                if (row == numRows - 1)
                    flag = -1;
                row += flag;
            }
            s.clear();
            for (int i = 0; i < numRows; i++)
                s += str[i];
            delete[] str;
            return s;
        }
    };    
#####总结：
* 没有考虑numRows <= 1的情况。
* 释放指针内存的习惯。
