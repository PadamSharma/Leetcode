# 2089. Find Target Indices After Sorting Array
**Easy**

You are given a 0-indexed integer array nums and a target element target.

A target index is an index i such that nums[i] == target.

Return a list of the target indices of nums after sorting nums in non-decreasing order. If there are no target indices, return an empty list. The returned list must be sorted in increasing order.

> Count occurance of target and elements in num less than target and append index++ while count-- becomes 0.

```c++
class Solution {
public:
    vector<int> targetIndices(vector<int>& nums, int target) {
        int c=0;int less=0;
        for(auto i:nums){
            c+= i==target;
            less+= i<target;
        }
        vector<int> ans;
        while(c--){
            ans.push_back(less++);
        }
        return ans;
    }
};
```

# 

```c++

```