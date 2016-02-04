##LeetCode解题报告
####15. 3Sum
#####题目内容：
***
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

<b>Note:</b>

Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)

The solution set must not contain duplicate triplets.   
    
    For example, given array S = {-1 0 1 2 -1 -4},

    A solution set is:
    (-1, 0, 1)
    (-1, -1, 2)

***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;先对数组进行排序，然后对每一个固定的数，用夹逼法找后两个数。
#####核心代码：
    class Solution
    {
    public:
        vector<vector<int>> threeSum(vector<int>& nums)
        {
            vector< vector<int> > result;
            int index = 0, head, tail, target;
        
            if (nums.size() < 3)
                return result;
            sort(nums.begin(), nums.end());
            while (index < nums.size())
            {
                target = -nums[index];
                if (target < 0)
                    break;
                head = index + 1, tail = (int)nums.size() - 1;
                while (head < tail)
                {
                    if (nums[head] + nums[tail] > target)
                        tail--;
                    else if (nums[head] + nums[tail] < target)
                        head++;
                    else
                    {
                        result.push_back({nums[index], nums[head++], nums[tail--]});
                        while (head < tail && nums[head] == nums[head - 1])
                            head++;
                        while (head < tail && nums[tail] == nums[tail + 1])
                            tail--;
                    }
                }
                index++;
                while (index < nums.size() && nums[index] == nums[index - 1])
                    index++;
            }
            return result;
        }
    };