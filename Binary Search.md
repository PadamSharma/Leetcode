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

# 1351. Count Negative Numbers in a Sorted Matrix
**Easy**

Given a m x n matrix grid which is sorted in non-increasing order both row-wise and column-wise, return the number of negative numbers in grid.

```c++
class Solution {
public:
    int countNegatives(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        int i = m-1, j = 0, c=0;
        while(i>=0){
            if(grid[i][j]<0){
                c+=n-j;
                i--;
            }
            else if(j+1>=n){
                j = 0;
                i--;
            }
            else{
                j++;
            }
        }
        return c;
    }
};
```