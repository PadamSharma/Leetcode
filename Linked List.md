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

# 2130. Maximum Twin Sum of a Linked List
**Medium**

In a linked list of size n, where n is even, the ith node (0-indexed) of the linked list is known as the twin of the (n-1-i)th node, if 0 <= i <= (n / 2) - 1.

    For example, if n = 4, then node 0 is the twin of node 3, and node 1 is the twin of node 2. These are the only nodes with twins for n = 4.

The twin sum is defined as the sum of a node and its twin.

Given the head of a linked list with even length, return the maximum twin sum of the linked list.

> Reverse the linked list upto half and then check for maximum.

```c++
class Solution {
public:
    int pairSum(ListNode* head) {
        if(!head->next->next){
            return head->val+head->next->val;
        }
        ListNode *slow = head, *fast = head;
        ListNode *nxt;
        ListNode *temp=NULL;
        while(fast && fast->next){
            fast = fast->next->next;
            nxt = slow->next;
            slow->next = temp;
            temp = slow;
            slow = nxt;
        }
        int ans=0;
        while(slow && temp){
            ans = max(ans, slow->val+temp->val);
            slow = slow->next;
            temp = temp->next;
        }
        return ans;
    }
};
```

# 1721. Swapping Nodes in a Linked List
**Medium**

You are given the head of a linked list, and an integer k.

Return the head of the linked list after swapping the values of the kth node from the beginning and the kth node from the end (the list is 1-indexed).

> If length is odd and k is in middle return the same list without swapping anything. 

> Else if k is greater than n/2 then reset it to value smaller than n/2.

> Else iterate over the list and find (k-1)th and (n-k)th node and then finally swap their values.


```c++
class Solution {
public:
    ListNode* swapNodes(ListNode* head, int k) {
        ListNode *kth=head, *n1kth=head;
        ListNode *temp = head;
        int idx=0;
        int n=0;
        while(temp){
            temp = temp->next;
            n++;
        }
        if(k-1==n-k){ // if n is odd and k is the middle element
            return head;
        }
        if(k>n/2){ // if k is greater than n/2 then reset k back to value less than n/2
            k = n-k+1;
        }
        while(idx<=(n-k)){
            if(idx<k-1){
                kth = kth->next;
                n1kth = n1kth->next;
            }
            else if(idx>=k-1 && idx<(n-k)){
                n1kth = n1kth->next;
            }
            idx++;
        }
        cout<<n1kth->val<<" - "<<n1kth->val<<endl;
        swap(kth->val, n1kth->val);
        return head;
    }
};
```

# 1019. Next Greater Node In Linked List
**Medium**

You are given the head of a linked list with n nodes.

For each node in the list, find the value of the next greater node. That is, for each node, find the value of the first node that is next to it and has a strictly larger value than it.

Return an integer array answer where answer[i] is the value of the next greater node of the ith node (1-indexed). If the ith node does not have a next greater node, set answer[i] = 0.

> Reverse linked list as we need to find the next greater element to the right.

> Use of stack becomes important as we need occurance of the first greater element. Thus we pop from stack until greater element is found and then push the same into it.

```c++
class Solution {
public:
    vector<int> nextLargerNodes(ListNode* head) {
        ListNode *nxt;
        ListNode *curr = NULL;
        int n=0;
        while(head){
            nxt = head->next;
            head->next = curr;
            curr = head;
            head = nxt;
            n++;
        }
        int mx=0,prev=0;
        vector<int> ans(n);
        stack<int> s;
        int i=0;
        while(curr){
            if (!s.empty()) {
                while (!s.empty() && s.top() <= curr->val) {
                    s.pop();
                }
            }
            ans[i] = s.empty() ? 0 : s.top();
            s.push(curr->val);
            curr = curr->next;
            i++;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

# 328. Odd Even Linked List
**Medium**

Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in O(1) extra space complexity and O(n) time complexity.

> Use even_head to store head for even nodes and then point the end of the odd list to this evenhead node.

> In the loop update the next nodes by skipping a node to get both odd and even nodes in respctive lists.

```c++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(!head){
            return head;
        }
        ListNode *evenhead = head->next, *odd = head, *even = evenhead;
        while(even && even->next){
            odd->next = odd->next->next;
            even->next = even->next->next;
            odd = odd->next;
            even = even->next;
        }
        odd->next = evenhead;
        return head;
    }
};
```

# 24. Swap Nodes in Pairs
Medium

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

> Ordering of operations is important :
> 
> 1. Create a dummy node to store head of the list to be returned
> 
> In the loop :
> 
> 2. Next of PREV points to Next of CURR (dummy points to second element of the list), to make it the head element (the first step).
> 3. Next of CURR (first element) points to Next of Next of PREV (third element)
> 4. Update the nodes : PREV to CURR & CURR to CURR->Next


```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next){
            return head;
        }
        ListNode *prev;
        ListNode *dummy = new ListNode();
        prev = dummy;
        ListNode *curr = head;
        while(curr && curr->next){
            prev->next = curr->next;
            curr->next = prev->next->next;
            prev->next->next = curr;
            
            prev = curr;
            curr = curr->next;
        }
        return dummy->next;
    }
};
```

# 445. Add Two Numbers II
Medium

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

> Terminate while loop when carry = 0 and all stacks are empty, otherwise continue.

> How n1 and n2 are calculated is important as we check on every iteration whether stack is empty or not, if it is not empty then n1 gets the value of top of stack, else stays 0. This way we don't need another loop to empty non empty stacks.

> Carry is calculated at the end of every iteration, then checked in the condition of the loop the used to calculate sum, then lastly updated at the end (ideal worflow for carry)

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> s1,s2;
        while(l1){
            s1.push(l1->val);
            l1 = l1->next;
        }
        while(l2){
            s2.push(l2->val);
            l2 = l2->next;
        }
        int c=0, n1=0, n2=0;
        ListNode *ans = NULL;
        while(!s1.empty() || !s2.empty() || c){
            if(!s1.empty()){
                n1 = s1.top();
                s1.pop();
            }
            else{
                n1 = 0;
            }
            if(!s2.empty()){
                n2 = s2.top();
                s2.pop();
            }
            else{
                n2 = 0;
            }
            ListNode *temp = new ListNode((n1+n2+c)%10);
            temp->next = ans;
            ans = temp;
            c = (n1+n2+c)/10;
        }
        return ans;
    }
};
```

# 817. Linked List Components
Medium

You are given the head of a linked list containing unique integer values and an integer array nums that is a subset of the linked list values.

Return the number of connected components in nums where two values are connected if they appear consecutively in the linked list.

For example : head = [0,1,2,3,4], nums = [0,3,1,4]

```diff
- > 0, 1
+ > 2,
- > 3, 5
```
> Here we need to sum up number of occurances of ends of those red connected components.

> Check for end of red components : 
> 
> * Check if current component is present in array, 
> * **AND** , 
> * if next node is null (end of list is reached) **OR** value of next node is not present in array.

```c++
class Solution {
public:
    int numComponents(ListNode* head, vector<int>& nums) {
        unordered_set<int> st(begin(nums), end(nums));
        int ans=0;
        while(head){
            if(st.count(head->val) && (!head->next || !st.count(head->next->val))){
                ans++;
            }
            head = head->next;
        }
        return ans;
    }
};
```

# 2058. Find the Minimum and Maximum Number of Nodes Between Critical Points
Medium

A critical point in a linked list is defined as either a local maxima or a local minima.

A node is a local maxima if the current node has a value strictly greater than the previous node and the next node.

A node is a local minima if the current node has a value strictly smaller than the previous node and the next node.

Note that a node can only be a local maxima/minima if there exists both a previous node and a next node.

Given a linked list head, return an array of length 2 containing [minDistance, maxDistance] where minDistance is the minimum distance between any two distinct critical points and maxDistance is the maximum distance between any two distinct critical points. If there are fewer than two critical points, return [-1, -1].

> Push indexes of critical points into a vector and then calculate minimum and maximum distances. 

```c++
class Solution {
public:
    bool critical(int a, int b, int c){
        if((b>a && b>c) || (b<a && b<c)){
            return true;
        }
        return false;
    }
    vector<int> nodesBetweenCriticalPoints(ListNode* head) {
        vector<int> ans = {-1,-1};
        if(!head->next->next){
            return ans;
        }
        int i=1;
        vector<int> idx;
        while(head && head->next && head->next->next){
            if(critical(head->val, head->next->val, head->next->next->val)){
                idx.push_back(i);
            }
            i++;
            head = head->next;
        }
        if(idx.size()>1){
            ans[1] = idx[idx.size()-1] - idx[0];
            int mn = INT_MAX;
            for(int i=1;i<idx.size();i++){
                mn = min(mn, idx[i] - idx[i-1]);
            }
            ans[0] = mn;
        }
        return ans;
    }
};
```

# 2095. Delete the Middle Node of a Linked List
Medium

You are given the head of a linked list. Delete the middle node, and return the head of the modified linked list.

The middle node of a linked list of size n is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

    For n = 1, 2, 3, 4, and 5, the middle nodes are 0, 1, 1, 2, and 2, respectively.

> If there is only one or two nodes handle them accordingly

>Else get the slow pointer and update the address of that pointer variable to the address of the next node

```c++
class Solution {
public:
    ListNode* deleteMiddle(ListNode* head) {
        if(!head->next){
            return NULL;
        }
        if(!head->next->next){
            head->next = nullptr;
            return head;
        }
        ListNode *temp = head;
        ListNode *slow = temp;
        ListNode *fast = temp;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }
        *slow = *(slow->next);
        return head;
    }
};
```