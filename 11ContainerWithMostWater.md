##LeetCode解题报告
####11. Container With Most Water
#####题目内容：
***
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;贪心法。因为容器的容量为两条线段的距离乘以最短线段的长度，所以用两个指针分别指向最左和最右边的线段，从最远距离开始枚举，每次移动更短线段上的指针，分别计算容量并更新最大值。
#####核心代码：
    class Solution 
    {
    public:
        int maxArea(vector<int>& height) 
        {
            int ans = 0;
            for (int head = 0, tail = height.size() - 1; head < tail;)
                ans = max(ans, (height[head] < height[tail]) ? 
                               ((tail - head) * height[head++]) : 
                               ((tail - head) * height[tail--]));
            return ans;
        }
    };