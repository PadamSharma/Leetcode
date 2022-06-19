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

# 203. Remove Linked List Elements
**Easy**

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

> Not used pointer variable to change address of the current node( Q.237 Delete current node in a linked list ) to next node as it is difficult to remove the last node if its value = val. Thus used common method to overwrite the address using next method only.

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode *temp = head;
        if(!head){
            return head;
        }
        while(head && head->val == val){
            head = head->next;
        }
        while(temp->next){
            if(temp->next->val == val){
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

# 2181. Merge Nodes in Between Zeros
**Medium**

You are given the head of a linked list, which contains a series of integers separated by 0's. The beginning and end of the linked list will have Node.val == 0.

For every two consecutive 0's, merge all the nodes lying in between them into a single node whose value is the sum of all the merged nodes. The modified list should not contain any 0's.

Return the head of the modified linked list.

```c++
class Solution {
public:
    ListNode* mergeNodes(ListNode* head) {
        ListNode *ans;
        ListNode *dummy = new ListNode();
        ans = dummy;
        int sum=0;
        head=head->next;
        while(head){
            if(head->val == 0){
                ListNode *temp = new ListNode(sum);
                ans->next = temp;
                ans = ans->next;
                sum=0;
            }
            else{
                sum+=head->val;
            }
            head=head->next;
        }
        return dummy->next;
    }
};
```

# 1669. Merge In Between Linked Lists
**Medium**

You are given two linked lists: list1 and list2 of sizes n and m respectively.

Remove list1's nodes from the ath node to the bth node, and put list2 in their place.

The blue edges and nodes in the following figure indicate the result:

Build the result list and return its head.

```c++
class Solution {
public:
    ListNode* mergeInBetween(ListNode* list1, int a, int b, ListNode* list2) {
        ListNode *bNode = list1;
        ListNode *ans = list1;
        int idx=0;
        while(idx<=b){
            bNode = bNode->next;
            idx++;
        }
        idx=0;
        while(list1->next && list2){
            if(idx==a-1){
                list1->next = list2;
            }
            if(idx>=a){
                list2 = list2->next;
            }
            list1 = list1->next;
            idx++;
        }
        list1->next = bNode;
        return ans;
    }
};
```