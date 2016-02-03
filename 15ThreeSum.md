##LeetCode解题报告
####16. 3Sum Closest
#####题目内容：
***
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;和15题一样的方法。
#####核心代码：
    class Solution
    {
    public:
        int threeSumClosest(vector<int>& nums, int target)
        {
            int result = nums[0] + nums[1] + nums[2];
            sort(nums.begin(), nums.end());
            for (int i = 0; i < nums.size() - 2; i++)
            {
                int head = i + 1, tail = (int)nums.size() - 1;
                while (head < tail)
                {
                    int tmp = nums[i] + nums[head] + nums[tail];
                    if (abs(tmp - target) < abs(result - target))
                        result = tmp;
                    if (result == target)
                        return target;
                    tmp < target ? head++ : tail--;
                }
            }
            return result;
        }
    };