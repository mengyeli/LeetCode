##LeetCode解题报告
####137. Single Number II
#####题目内容：
***
Given an array of integers, every element appears three times except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;考虑二进制，如果每个数出现三次，那么二进制每一位上1出现的次数也应该正好是3的整数倍。所以统计二进制每一位上1出现的次数，如果不是3的整数倍，说明要找的数的二进制在那一位上为1，否则为0。

#####核心代码：
	int singleNumber(vector<int>& nums) 
    {
        const int INT = sizeof(int) * 8;
        int count[INT], ans = 0;
        memset(count, 0, sizeof(count));
        for (int i = 0; i < nums.size(); i++)
        {
            for (int j = 0; j < INT; j++)
            {
                count[j] += (nums[i] >> j) & 1;
                count[j] %= 3;
            }
        }
        for (int i = 0; i < INT; i++)
            ans += (count[i] << i);
        return ans;
    }

#####拓展：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;此类问题可以归结为：给一列数，除了一个数出现m次以外，其他数都出现k次，找到这个数。对于本题来讲，k = 3，m = 1。用a，b两位来表示三种状态{00, 01, 10}，则状态转移式为：a = (a&~b&~c)|(~a&b&c)，b= (~a&b&~c)|(~a&~b&c)，a|b即为所求。具体内容详见参考资料。

#####参考资料：
1. https://leetcode.com/discuss/54970/an-general-way-to-handle-all-this-sort-of-questions

