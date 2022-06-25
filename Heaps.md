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

# 1338. Reduce Array Size to The Half
**Medium**

You are given an integer array arr. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return the minimum size of the set so that at least half of the integers of the array are removed.

> Minimum size of array is achieved when integers which have minimum count are removed such that resultant array has size less than half of the original and its set contains minimum number of elements.

> Unordered map stores the count of the integers and priority queue gives the count in descending order, so we can keep the count of the integers which have higher count and we can form the array with them such that its size is less than half of the original and also it can contain minimum number of unique integers.

```c++
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        unordered_map<int, int> mp;
        priority_queue<int> pq;
        for(auto i:arr){
            mp[i]++;
        }
        for(auto i:mp){
            pq.push(i.second);
        }
        int ans=0, c=0;
        while(c*2<arr.size()){
            c+=pq.top();
            pq.pop();
            ans++;
        }
        return ans;
    }
};
```

# 692. Top K Frequent Words
**Medium**

Given an array of strings words and an integer k, return the k most frequent strings.

Return the answer sorted by the frequency from highest to lowest. Sort the words with the same frequency by their lexicographical order.

> Pairs can be used with priority queues, such that first element of the pair is considered by PQ.

> PQ.emplace saves the unnecessary space which is used by simple PQ.push which creates the object of the element to be pushed and then insert into PQ.

> Also as first element is negative so pairs with smaller count are at the top of the PQ, thus as the size of the PQ becomes >= k we can pop the top from PQ.

> Save the second of the pair in the ans vector as PQ is currently working as MIN HEAP for us(as count stored as first in pair is negative).

```c++
class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        map<string, int> mp;
        for(auto i:words){
            mp[i]++;
        }
        priority_queue<pair<int, string>> pq;
        for(auto i:mp){
            pq.emplace(-i.second, i.first);
            if(pq.size()>k){
                pq.pop();
            }
        }
        vector<string> ans(pq.size());
        for(int i=pq.size()-1;i>=0;i--){
            ans[i] = (pq.top()).second;
            pq.pop();
        }
        return ans;
    }
};
```

# 973. K Closest Points to Origin
**Medium**

Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., 
$$ √(x1 - x2)2 + (y1 - y2)2) $$

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

```c++
class Solution {
public:
    int dist(vector<int> coord){
        return (coord[0]*coord[0]) + (coord[1]*coord[1]);
    }
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        unordered_map<int, int> mp;
        for(auto i=0;i<points.size();i++){
            mp[i] = dist(points[i]);
        }
        priority_queue<pair<int, int>> pq;
        for(auto i:mp){
            pq.push({-i.second, i.first});
        }
        vector<vector<int>> ans;
        while(k--){
            ans.push_back(points[pq.top().second]);
            pq.pop();
        }
        return ans;
    }
};
```

# 1753. Maximum Score From Removing Stones
Medium

You are playing a solitaire game with three piles of stones of sizes a​​​​​​, b,​​​​​​ and c​​​​​​ respectively. Each turn you choose two different non-empty piles, take one stone from each, and add 1 point to your score. The game stops when there are fewer than two non-empty piles (meaning there are no more available moves).

Given three integers a​​​​​, b,​​​​​ and c​​​​​, return the maximum score you can get.

> Top of max heap gives max of the 3 elements, thus take that top 2 elements from PQ, decrement them and push back into PQ if those are still greater than 0. Thus we maintain the max elements and simulate the process as in the problem.

```c++
class Solution {
public:
    int maximumScore(int a, int b, int c) {
        priority_queue<int> pq;
        int ans=0;
        pq.push(a);
        pq.push(b);
        pq.push(c);
        while(pq.size()>1){
            int i = pq.top();
            pq.pop();
            int j = pq.top();
            pq.pop();
            if(--i > 0){
                pq.push(i);
            }
            if(--j > 0){
                pq.push(j);
            }
            ans++;
        }
        return ans;
    }
};
```

# 347. Top K Frequent Elements
**Medium**

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        for(auto i:nums) mp[i]++;
        priority_queue<pair<int, int>> pq;
        for(auto i:mp){
            pq.emplace(-i.second, i.first);
            if(pq.size()>k){
                pq.pop();
            }
        }
        vector<int> ans(pq.size());
        for(int i=pq.size()-1; i>=0;i--){
            ans[i] = pq.top().second;
            pq.pop();
        }
        return ans;
    }
};
```

# 215. Kth Largest Element in an Array
**Medium**

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

> Runtime : 20ms

> Priority queue can have same integer repeated, so creating a priority queue over the input array is the best  option.

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        for(auto i:nums) mp[i]++;
        priority_queue<pair<int, int>> pq;
        for(auto i:mp){
            pq.emplace(i.first, i.second);
        }
        int ans=0, i=0;
        while(pq.size()){
            ans = pq.top().first;
            i+=pq.top().second;
            if(i>=k){
                break;
            }
            pq.pop();
        }
        return ans;
    }
}
```

> Runtime : 7ms

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> pq = {begin(nums), end(nums)};
        k--;
        while(k--) pq.pop();
        return pq.top();
    }
};
```

# 1738. Find Kth Largest XOR Coordinate Value
**Medium**

You are given a 2D matrix of size m x n, consisting of non-negative integers. You are also given an integer k.

The value of coordinate (a, b) of the matrix is the XOR of all matrix[i][j] where 0 <= i <= a < m and 0 <= j <= b < n (0-indexed).

Find the kth largest value (1-indexed) of all the coordinates of matrix.

![](https://assets.leetcode.com/users/images/39c6c67f-63da-44af-8899-84c5a4e21239_1611457938.8521633.png) ----------> ![](https://assets.leetcode.com/users/images/a1f2e8ad-36a5-492f-abd5-ec15ed4f8fd1_1611457955.8021202.png) ----------> ![](https://assets.leetcode.com/users/images/1dec0d1d-6a5e-4a20-9578-efba40afd03c_1611458472.0484324.png)

```c++
class Solution {
public:
    int kthLargestValue(vector<vector<int>>& matrix, int k) {
        for(int i=1;i<matrix.size();i++){
            for(int j=0;j<matrix[0].size();j++){
                matrix[i][j]^=matrix[i-1][j];
            }
        }
        for(int i=0;i<matrix.size();i++){
            for(int j=1;j<matrix[0].size();j++){
                matrix[i][j]^=matrix[i][j-1];
            }
        }
        priority_queue<int> pq;
        for(int i=0;i<matrix.size();i++){
            for(int j=0;j<matrix[0].size();j++){
                pq.push(matrix[i][j]);
            }
        }
        k--;
        while(k--){
            pq.pop();
        }
        return pq.top();
    }
};
```

# 912. Sort an Array
**Medium**

Given an array of integers nums, sort the array in ascending order.

```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        priority_queue<int> pq;
        for(auto i:nums){
            pq.push(-i);
        }
        for(auto &i:nums){
            i = -pq.top();
            pq.pop();
        }
        return nums;
    }
};
```

# 1962. Remove Stones to Minimize the Total
**Medium**

You are given a 0-indexed integer array piles, where piles[i] represents the number of stones in the ith pile, and an integer k. You should apply the following operation exactly k times:

    Choose any piles[i] and remove floor(piles[i] / 2) stones from it.

Notice that you can apply the operation on the same pile more than once.

Return the minimum possible total number of stones remaining after applying the k operations.

floor(x) is the greatest integer that is smaller than or equal to x (i.e., rounds x down).

> We need to use what we know, here in this problem we know the initial sum, and the operation decribed in the problem decreases that sum by element/2

> Thus if we keep account of this we can cut off another loop over PQ for calulating the sum, hence bringing down Runtime from 1200ms to 600ms.

```c++
class Solution {
public:
    int minStoneSum(vector<int>& piles, int k) {
        priority_queue<int> pq(begin(piles), end(piles));
        int ans = accumulate(begin(piles), end(piles), 0);;
        while(k--){
            pq.push(pq.top() - floor(pq.top()/2));
            ans-=floor(pq.top()/2);
            pq.pop();
        }
        return ans;
    }
};
```

# 

```c++

```