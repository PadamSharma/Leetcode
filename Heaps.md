# 1464. Maximum Product of Two Elements in an Array
**Easy**

Given the array of integers nums, you will choose two different indices i and j of that array. Return the maximum value of (nums[i]-1)*(nums[j]-1).

```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        priority_queue<int> pq;
        for(auto i:nums){
            pq.push(i);
        }
        int x=pq.top(); pq.pop();
        int y=pq.top();
        return (x-1)*(y-1);
    }
};
```

# 1337. The K Weakest Rows in a Matrix
**Easy**

You are given an m x n binary matrix mat of 1's (representing soldiers) and 0's (representing civilians). The soldiers are positioned in front of the civilians. That is, all the 1's will appear to the left of all the 0's in each row.

A row i is weaker than a row j if one of the following is true:

The number of soldiers in row i is less than the number of soldiers in row j.
Both rows have the same number of soldiers and i < j.
Return the indices of the k weakest rows in the matrix ordered from weakest to strongest.

> Use multimap to store pair of sum, index : As map stores pairs in sorted order just iterate over k elements and return vector.

```c++
class Solution {
public:
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        multimap<int, int> map;
        int j=0;
        vector<int> ans;
        for(auto i:mat){
            map.insert({accumulate(i.begin(),i.end(),0), j});
            j++;
        }
        for(auto i = map.begin();k>0;k--,i++){
            ans.push_back(i->second);
        }
        return ans;
    }
};
```

# 1046. Last Stone Weight
**Easy**

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose the heaviest two stones and smash them together. Suppose the heaviest two stones have weights x and y with x <= y. The result of this smash is:

If x == y, both stones are destroyed, and
If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.
At the end of the game, there is at most one stone left.

Return the smallest possible weight of the left stone. If there are no stones left, return 0.

```c++
class Solution {
public:
    int lastStoneWeight(vector<int>& stones) {
        priority_queue<int> pq;
        for(auto i:stones){
            pq.push(i);
        }
        while(pq.size() > 1){
            int x = pq.top(); pq.pop();
            int y = pq.top(); pq.pop();
            pq.push(abs(x-y));
        }
        return pq.top();
    }
};
```

# 2231. Largest Number After Digit Swaps by Parity
**Easy**

You are given a positive integer num. You may swap any two digits of num that have the same parity (i.e. both odd digits or both even digits).

Return the largest possible value of num after any number of swaps.

```c++
class Solution {
public:
    int largestInteger(int num) {
        priority_queue<int> e;
        priority_queue<int> o;
        vector<int> nums;
        while(num){
            int d = num%10;
            nums.push_back(d);
            num/=10;
        }
        for(auto& i:nums){
            if(i%2){
                o.push(i*-1);
            }
            else{
                e.push(i*-1);
            }
            i = i%2;
        }
        for(auto& i:nums){
            if(i){
                i = o.top();
                o.pop();
            }
            else{
                i = e.top();
                e.pop();
            }
        }
        reverse(nums.begin(), nums.end());
        int ans=0;
        for(auto i:nums){
            ans*=10;
            ans+=(i)*-1;
            
        }
        return ans;
        
    }
};
```

# 506. Relative Ranks
**Easy**

You are given an integer array score of size n, where score[i] is the score of the ith athlete in a competition. All the scores are guaranteed to be unique.

The athletes are placed based on their scores, where the 1st place athlete has the highest score, the 2nd place athlete has the 2nd highest score, and so on. The placement of each athlete determines their rank:

The 1st place athlete's rank is "Gold Medal".
The 2nd place athlete's rank is "Silver Medal".
The 3rd place athlete's rank is "Bronze Medal".
For the 4th place to the nth place athlete, their rank is their placement number (i.e., the xth place athlete's rank is "x").
Return an array answer of size n where answer[i] is the rank of the ith athlete.

```c++
class Solution {
public:
    vector<string> findRelativeRanks(vector<int>& score) {
        priority_queue<int> pq;
        for(auto i:score){
            pq.push(i);
        }
        int c=0;
        unordered_map<int, string> map;
        while(!pq.empty()){
            if(c==0){
                map[pq.top()] = "Gold Medal";
            }
            else if(c==1){
                map[pq.top()] = "Silver Medal";
            }
            else if(c==2){
                map[pq.top()] = "Bronze Medal";
            }
            else{
                map[pq.top()] = to_string(c+1);
            }
            c++;
            pq.pop();
        }
        vector<string> ans;
        for(auto i:score){
            ans.push_back(map[i]);
        }
        return ans;
    }
};
```

# 2099. Find Subsequence of Length K With the Largest Sum
**Easy**

You are given an integer array nums and an integer k. You want to find a subsequence of nums of length k that has the largest sum.

Return any such subsequence as an integer array of length k.

A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

```c++
class Solution {
public:
    vector<int> maxSubsequence(vector<int>& nums, int k) {
        priority_queue<int> pq;
        for(auto i:nums){
            pq.push(i);
        }
        int k_ = k;
        unordered_map<int,int> map;
        while(k){
            map[pq.top()]++;
            pq.pop();
            k--;
        }
        vector<int> ans;
        for(auto i:nums){
            if(map[i]){
                map[i]--;
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```