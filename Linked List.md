# 1290. Convert Binary Number in a Linked List to Integer
**Easy**

Given head which is a reference node to a singly-linked list. The value of each node in the linked list is either 0 or 1. The linked list holds the binary representation of a number.

Return the decimal value of the number in the linked list.

```c++
class Solution {
public:
    int getDecimalValue(ListNode* head) {
        ListNode *temp = head;
        int ans=0;
        while(temp){
            ans=ans*2 + temp->val;
            temp = temp->next;
        }
        return ans;
    }
};
```

# 237. Delete Node in a Linked List
**Easy**

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

> *node contains address of node variable and we are updating the address of node with address of node->next.

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        *node = *node->next;
    }
};
```

# 206. Reverse Linked List
**Easy**

Given the head of a singly linked list, reverse the list, and return the reversed list.

> If the list is either empty or contains single node, return head. Otherwise maintain two variables to store next node and the current node. 
* **nxt = head -> next**, store the next node
* **head -> next = curr**, make head node point to current node, which initially was set to NULL,
* **curr = head**, set current node to head thus move forward in list as in next operation,
* **head = nxt**, nxt becomes the head node, hence we move forward in Linked List.

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head){
            return head;
        }
        else if(!head->next){
            return head;
        }
        else{
            ListNode *nxt, *curr = NULL;
            while(head){
                nxt = head->next;
                head->next = curr;
                curr = head;
                head = nxt;
            }
            return curr;
        }
    }
};
```

# 237. Delete Node in a Linked List
**Easy**

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

> Using \* operator we can overwrite the address of the given node with the address of its next node.

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        *node = *node->next;
    }
};
```

# 21. Merge Two Sorted Lists
**Easy**

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

> Dummy variable stores the address of the new merged Linked List. Simply compare and add nodes to the new list then return the node pointing to the head of this list.

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *temp, *dummy = new ListNode();
        temp = dummy; // stores the address of first node of temp list
        while(list1 && list2){
            if(list1->val < list2->val){
                temp->next = list1;
                list1 = list1->next;
                
            }
            else{
                temp->next = list2;
                list2 = list2->next;
            }
            temp = temp->next;
        }
        if(list1){
            temp->next = list1;
        }
        else{
            temp->next = list2;
        }
        return dummy->next;
    }
};
```

# 83. Remove Duplicates from Sorted List
**Easy**

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

```c++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *temp = head;
        while(temp && temp->next){
            if(temp->val == temp->next->val){
                temp->next = temp->next->next;
            }
            else{
                temp = temp->next;
            }
        }
        return head;
    }
};
```

# 141. Linked List Cycle
**Easy**

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *slow=head, *fast=head;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
            if(slow == fast){
                return true;
            }
        }
        return false;
    }
};
```

# 234. Palindrome Linked List
Easy

Given the head of a singly linked list, return true if it is a palindrome.

> Reverse Linked List and check if fast pointer is NULL or not if it is !NULL then move slow pointer one step as the length of the list is even.

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode *slow=head, *fast=head;
        ListNode *temp=NULL;
        ListNode *nxt;
        while(fast && fast->next){
            fast=fast->next->next;
            nxt = slow->next;
            slow->next=temp;
            temp=slow;
            slow=nxt;
        }
        if(fast){
            slow = slow->next;
        }
        while(temp && slow){
            if(temp->val!=slow->val){
                return false;
            }
            temp = temp->next;
            slow = slow->next;
        }
        return true;
    }
};
```

# 

```c++

```