##LeetCode解题报告
####2. Add Two Numbers

#####题目内容：
***
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8
***
#####解题思路：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;模拟列竖式加法的过程即可。
#####核心代码：
	ListNode* addTwoNumbers(ListNode* l1, ListNode* l2)
    {
        ListNode *ans = new ListNode(0);
        ListNode *tmp = ans, *prev;
        int rest = 0;
        while (l1 || l2 || rest)
        {
            if (l1)
            {
                rest += l1->val;
                l1 = l1->next;
            }
            if (l2)
            {
                rest += l2->val;
                l2 = l2->next;
            }
            tmp->val = rest % 10;
            rest /= 10;
            tmp->next = new ListNode(rest);
            prev = tmp;
            tmp = tmp->next;
        }
        prev->next = NULL;
        return ans;
    }
