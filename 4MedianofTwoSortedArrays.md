##LeetCode解题报告
####4. Median of Two Sorted Arrays
#####题目内容：
***
There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).
***

#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;由于数组有序，很容易想到将两个数组看成两个队列，每次判断两个队首元素，出队较小的那个即可。时间复杂度为O((m + n) / 2)。由于题目要求为O(log (m+n))，所以考虑用二分法优化，每次出队一半的元素。

#####核心代码：
	double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        int n = (int)nums1.size();
        int m = (int)nums2.size();
        int done = 0, next = ((n + m) >> 2), tmpn = 0, tmpm = 0, target = ((n + m) >> 1);
        if ((n + m) % 2 == 0)
            target--;
        nums1.push_back(1 << 30);
        nums1.push_back(1 << 30);
        nums2.push_back(1 << 30);
        nums2.push_back(1 << 30);
        while (done < target)
        {
            int x = nums1[tmpn + next - 1];
            int y = nums2[tmpm + next - 1];
            if (x < y)
                tmpn += next;
            else
                tmpm += next;
            done += next;
            next = next >> 1;
            if (!next)
                next = 1;
        }
        int a[4];
        a[0] = nums1[tmpn];
        a[1] = nums1[tmpn + 1];
        a[2] = nums2[tmpm];
        a[3] = nums2[tmpm + 1];
        sort(a, a + 4);
        nums1.pop_back();
        nums1.pop_back();
        nums2.pop_back();
        nums2.pop_back();
        if ((n + m) % 2)
            return a[0];
        else
            return (double)(a[0] + a[1]) / 2;
    }

#####总结：
* 注意分奇数偶数两种情况讨论。
* 在两个数组的最后都添加两个极大值，可以免去判断数组越界和数组为空这两种特殊情况。
* 此题用递归写或许会更简洁。以前做题怕栈溢出所以尽量不写递归，导致递归用的不多，有时间可以尝试再写一个递归版本。