##LeetCode解题报告
####1. Two Sum
#####题目内容：
***
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;一种方法是先对数组内的元素进行排序，然后定义两个指针，分别指向数组的头部和尾部，向中间逼近，直到两个指针指向元素的和与目标数相等。时间复杂度O(nlogn)。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;另一种方法是，在遍历数组的过程中，对于每一个元素x，用另一个数组来记录target - x，如果接下来再遇到target - x，则可以和前面的x组成答案。时间复杂度O(n)。
#####核心代码：
	vector<int> twoSum(vector<int>& nums, int target) 
    {
        static int MAX = 99999;
        static int DELT = 49999;
        vector<int> ans;
        int x[MAX];
        memset(x, 0, sizeof(x));
        for (int i = 0; i < nums.size(); i++)
        {
            if (x[nums[i] + DELT])
            {
                ans.push_back(((i + 1) < x[nums[i] + DELT] ? (i + 1) : x[nums[i] + DELT]));
                ans.push_back(((i + 1) > x[nums[i] + DELT] ? (i + 1) : x[nums[i] + DELT]));
                return ans;
            }
            x[target - nums[i] + DELT] = i + 1;
        }
    }

#####总结：
1. 在开始做的时候，没有考虑负数，所以第一次提交没有过。
2. 可以用哈希法扩大数据范围。
