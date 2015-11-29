##LeetCode解题报告
####136. Single Number

#####题目内容：
***
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;根据题意，除了要找的那个数以外，其他的数都出现了两次。考虑到两个相同数的异或为零；一个数异或零等于它本身。所以所有数的异或和即为答案。
#####核心代码：
	int singleNumber(vector<int>& nums) 
    {
        int ans = 0;
        vector<int>::iterator it;
        for (it = nums.begin(); it != nums.end(); it++)
            ans = ans xor *it;
        return ans;
    }
#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;开始的时候假设所求数为n，得出(sum + x) / 2 = (sum - x) / 2 + x，发现两边都约掉了0.0。然后想到了二进制，顺利解决此题。