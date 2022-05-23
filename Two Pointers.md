# 832. Flipping an Image
**Easy**

Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.

For example, flipping [1,1,0] horizontally results in [0,1,1].
To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0.

For example, inverting [0,1,1] results in [1,0,0].

```c++
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& image) {
        for(auto& v:image){
            int i=0,j=v.size()-1;
            while(i<=j){
                int temp = v[i];
                v[i] = !v[j];
                v[j] = !temp;
                i++;
                j--;
            }
        }
        return image;
    }
};
```

# 2108. Find First Palindromic String in the Array
**Easy**

Given an array of strings words, return the first palindromic string in the array. If there is no such string, return an empty string "".

A string is palindromic if it reads the same forward and backward.

```c++
class Solution {
public:
    string firstPalindrome(vector<string>& words) {
        string ans="";
        for(auto w:words){
            int i=0,j=w.length()-1;
            int c=0;
            while(i<=j){
                if(w[i]==w[j]){
                    c++;
                }
                else{
                    break;
                }
                i++;
                j--;
            }
            cout<<c<<endl;
            if(c==int((w.length()+1)/2)){
                ans=w;
                break;
            }
        }
        return ans;
    }
};
```

# 557. Reverse Words in a String III
**Easy**

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        w = s.split(' ')
        ans = ""
        for i in w:
            ans+=i[::-1]+" "
        return ans[:-1]
```

# 2000. Reverse Prefix of Word
**Easy**

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

For example, if word = "abcdefd" and ch = "d", then you should reverse the segment that starts at 0 and ends at 3 (inclusive). The resulting string will be "dcbaefd".
Return the resulting string.

```c++
class Solution {
public:
    string reversePrefix(string word, char ch) {
        int i=0;
        for(auto c:word){
            if(c==ch){
                break;
            }
            i++;
        }
        if(i<word.length()){
            reverse(word.begin(), word.begin()+i+1);
        }
        return word;
    }
};
```

# 942. DI String Match
**Easy**

A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:

s[i] == 'I' if perm[i] < perm[i + 1], and
s[i] == 'D' if perm[i] > perm[i + 1].
Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return any of them.

```c++
class Solution {
public:
    vector<int> diStringMatch(string s) {
        vector<int> n(s.length()+1, 0);
        int i=0,d=s.length();
        for(int j=0;j<s.length();j++){
            if(s[j] == 'I'){
                n[j]=i;
                i++;
            }
            else{
                n[j]=d;
                d--;
            }
        }
        if(s[s.length()-1]=='I'){
            n[s.length()] = d;
        }
        else{
            n[s.length()] = i;
        }
        return n;
    }
};
```

# 1768. Merge Strings Alternately
**Easy**

You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

```c++
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        string ans;
        int m = min(word1.length(), word2.length());
        for(int i=0;i<m;i++){
            ans+=word1[i];
            ans+=word2[i];
        }
        if(m>=word1.length()){
            for(int i=m;i<word2.length();i++){
                ans+=word2[i];
            }
        }
        else{
            for(int i=m;i<word1.length();i++){
                ans+=word1[i];
            }
        }
        return ans;
    }
};
```

# 905. Sort Array By Parity
**Easy**

Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

```c++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& nums) {
        int i=0,j=nums.size()-1;
        while(i<=j){
            if(nums[i]%2 && nums[j]%2==0){
                swap(nums[i], nums[j]);
            }
            if(nums[i]%2==0){
                i++;
            }
            else if(nums[j]%2){
                j--;
            }
        }
        return nums;
    }
};
```

# 344. Reverse String
**Easy**

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int i=0,j=s.size()-1;
        while(i<=j){
            swap(s[i],s[j]);
            i++;
            j--;
        }
    }
};
```

# 876. Middle of the Linked List
**Easy**

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

```c++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```

# 977. Squares of a Sorted Array
**Easy**

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int i=0,j=nums.size()-1;
        vector<int> ans;
        while(i<=j){
            if(abs(nums[i]) <= abs(nums[j])){
                ans.push_back(nums[j]*nums[j]);
                j--;
            }
            else{
                ans.push_back(nums[i]*nums[i]);
                i++;
            }
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

# 

```c++

```