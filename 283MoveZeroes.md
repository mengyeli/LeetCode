##LeetCode解题报告
####283. Move Zeroes

#####题目内容：
***
Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`.

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;首先定义一个指针变量flag，开始时指向第一个元素。然后遍历数组nums，如果当前元素不为0，则将其赋值给flag指向的元素，然后指针向后移动。当数组遍历结束时，将flag指向的元素之后的所有数都赋值为0即可。时间复杂度O(n)，没有额外开辟空间存储数组。

#####核心代码：
	void moveZeroes(vector<int>& nums) 
    {
        int flag = 0;
        for (int i = 0; i < nums.size(); i++)
            if (nums[i] != 0)
                nums[flag++] = nums[i];
        for (int i = flag; i < nums.size(); i++)
            nums[i] = 0;
    }