# 2160. Minimum Sum of Four Digit Number After Splitting Digits
**Easy**

You are given a positive integer num consisting of exactly four digits. Split num into two new integers new1 and new2 by using the digits found in num. Leading zeros are allowed in new1 and new2, and all the digits found in num must be used.

    For example, given num = 2932, you have the following digits: two 2's, one 9 and one 3. Some of the possible pairs [new1, new2] are [22, 93], [23, 92], [223, 9] and [2, 329].

Return the minimum possible sum of new1 and new2.

```c++
class Solution {
public:
    int minimumSum(int num) {
        vector<int> n;
        while(num){
            int d=num%10;
            n.push_back(d);
            num/=10;
        }
        sort(n.begin(), n.end());
        return (n[0]*10+n[2]+n[1]*10+n[3]);
    }
};
```

# 1221. Split a String in Balanced Strings
**Easy**

Balanced strings are those that have an equal quantity of 'L' and 'R' characters.

Given a balanced string s, split it in the maximum amount of balanced strings.

Return the maximum amount of split balanced strings.

```c++
class Solution {
public:
    int balancedStringSplit(string s) {
        int b=0, ans=0;
        for(auto i:s){
            if(i=='L'){
                b--;
            }
            else if(i=='R'){
                b++;
            }
            if(b==0){
                ans++;
            }
        }
        return ans;
    }
};
```

# 1323. Maximum 69 Number
Easy

You are given a positive integer num consisting only of digits 6 and 9.

Return the maximum number you can get by changing at most one digit (6 becomes 9, and 9 becomes 6).

```c++
class Solution {
public:
    int maximum69Number (int num) {
        vector<int> n;
        while(num){
            int d=num%10;
            n.push_back(d);
            num/=10;
        }
        reverse(n.begin(), n.end()); 
        // running loop reverse is a way to remove reverse but I am lazy to write loops...
        for(auto& i:n){
            if(i==6){
                i=9;
                break;
            }
        }
        int ans=0;
        // lazy as a lion
        reverse(n.begin(), n.end());
        for(auto i=0;i<n.size();i++){
            ans+=n[i]*int(pow(10,i));
        }
        return ans;
    }
};
```

# 1827. Minimum Operations to Make the Array Increasing
**Easy**

You are given an integer array nums (0-indexed). In one operation, you can choose an element of the array and increment it by 1.

    For example, if nums = [1,2,3], you can choose to increment nums[1] to make nums = [1,3,3].

Return the minimum number of operations needed to make nums strictly increasing.

An array nums is strictly increasing if nums[i] < nums[i+1] for all 0 <= i < nums.length - 1. An array of length 1 is trivially strictly increasing.

```c++
class Solution {
public:
    int minOperations(vector<int>& nums) {
        int op=0;
        if(nums.size()<=1){
            return op;
        }
        else{
            for(int i=0;i<nums.size()-1;i++){
                if(nums[i]>=nums[i+1]){
                    op+=(nums[i]+1-nums[i+1]);
                    nums[i+1]+=(nums[i]-nums[i+1]+1);
                }   
            }
        }
        return op;
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
        int ii=0,d=s.length();
        vector<int> ans;
        for(auto i:s){
            if(i=='I'){
                ans.push_back(ii);
                ii++;
            }
            else{
                ans.push_back(d);
                d--;
            }
        }
        if(s[s.length()-1]=='I'){
            ans.push_back(ii);
        }
        else{
            ans.push_back(d);
        }
        return ans;
    }
};
```

# 561. Array Partition I
**Easy**

Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.

```c++
class Solution {
public:
    int arrayPairSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
// bucket sort preferable as we know the constraints for element of array -O(n) instead of O(n.logn)
        int ans=0;
        for(int i=0;i<nums.size()-1;i+=2){
            ans+=(min(nums[i], nums[i+1]));
        }
        return ans;
    }
};
```

# 1217. Minimum Cost to Move Chips to The Same Position
**Easy**

We have n chips, where the position of the ith chip is position[i].

We need to move all the chips to the same position. In one step, we can change the position of the ith chip from position[i] to:

    position[i] + 2 or position[i] - 2 with cost = 0.
    position[i] + 1 or position[i] - 1 with cost = 1.

Return the minimum cost needed to move all the chips to the same position.

```c++
class Solution {
public:
    int minCostToMoveChips(vector<int>& position) {
        vector<int> ans(2,0);
        for(auto i:position){
            ans[i&1]++;
        }
        return min(ans[0], ans[1]);
    }
};
```

# 

```c++

```