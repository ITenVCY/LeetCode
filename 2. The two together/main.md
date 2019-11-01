```c++
/*
	You are given two non-empty linked lists representing two non-negative integers. 
	The digits are stored in reverse order and each of their nodes contain a single digit. 
	Add the two numbers and return it as a linked list.
	You may assume the two numbers do not contain any leading zero, except the number 0 itself.
	输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
	输出：7 -> 0 -> 8
	原因：342 + 465 = 807
*/

#include <iostream>

using namespace std;

struct ListNode {
	int val;
	ListNode *next;

	ListNode(int x) : val(x), next(NULL)
	{

	}
	
};

class Solution {
public:
	ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		if (!l1) { return l2; } //返回原列表当返回列表改变值的时候也会引起原列表的改变
		if (!l2) { return l1; }
		int c = 0;
		ListNode dummy(-1);
		ListNode* p = &dummy;
		for (; l1 || l2; p = p->next) {
			const int a = l1 ? l1->val : 0;
			const int b = l2 ? l2->val : 0;
			const int sum = a + b + c;
			p->next = new ListNode(sum % 10);
			c = sum / 10;
			l1 = l1 ? l1->next : nullptr;
			l2 = l2 ? l2->next : nullptr;
		}
		if (c) {
			p->next = new ListNode(c);
		}
		return dummy.next;
	}
};

void print(ListNode* Node)
{
	while (Node)
	{
		cout << Node->val << endl;
		Node = Node->next;
	}
}

int main()
{
	ListNode *p1, *p2 = NULL,*oldhead;

	ListNode a1(1), a2(2), a3(3);
	a1.next = &a2;
	a2.next = &a3;

	p1 = &a1;
	oldhead = p1;

	Solution s1;

	ListNode* newHead = s1.addTwoNumbers(p1, p2);
	newHead->val += 1;

	print(newHead);
	print(oldhead);

	return 0;
}
```

