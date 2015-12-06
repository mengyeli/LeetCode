##LeetCode解题报告
####3. Longest Substring Without Repeating Characters
#####题目内容：
***
Given a string, find the length of the longest substring without repeating characters. 

For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;用head和tail两个指针分别指向当前字串的头和尾，用x['i']记录字母i是否在当前字串中。每次将tail向后移动一位，如果tail指向的字母之前出现过，则将head指针移到那个字母的后边。不断更新字串长度，记录最大值即可。
#####核心代码：
	int lengthOfLongestSubstring(string s)
    {
        if (s.size() == 0)
            return 0;
        if (s.size() == 1)
            return 1;
        int ans = 1, head = 0, tail = 1, now = 1;
        bool x[999];
        memset(x, 0, sizeof(x));
        x[s[0]] = true;
        for (;tail < s.size(); tail++)
        {
            if (!x[s[tail]])
            {
                now++;
                ans = now > ans ? now : ans;
                x[s[tail]] = true;
            }
            else
            {
                while (s[head] != s[tail])
                {
                    x[s[head]] = false;
                    head++;
                    now--;
                }
                head++;
            }
        }
        return ans;
    }

#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;没有考虑字符串长度为空的情况。
