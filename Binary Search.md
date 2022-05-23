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

# 852. Peak Index in a Mountain Array
**Easy**

Let's call an array arr a mountain if the following properties hold:

    arr.length >= 3
    There exists some i with 0 < i < arr.length - 1 such that:
        arr[0] < arr[1] < ... arr[i-1] < arr[i]
        arr[i] > arr[i+1] > ... > arr[arr.length - 1]

Given an integer array arr that is guaranteed to be a mountain, return any i such that arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1].

> Do bin search such that if mid element is less than its successor then update left as mid+1 else update right as mid (not as mid-1, as it will not capture the actual max element). The algo works as, if mid is smaller than successor then max occurs in right so update left to mid+1 and if it is false then max is to the left of mid so update right as mid.

```c++
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int l=0,r=arr.size()-1;
        while(l<r){
            int mid =l+(r-l)/2;
            if(arr[mid]<arr[mid+1]){
                l = mid+1;
            }
            else{
                r = mid;
            }
        }
        return r;
    }
};
```

# 349. Intersection of Two Arrays
**Easy**

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

> Erase from set removes the element from the set of nums1 and then we can append in ans. If element of same value pops up then it is discarded as the same value got erased earlier.

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> set(nums1.begin(), nums1.end());
        vector<int> ans;
        for(auto i:nums2){
            if(set.erase(i)){
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```

# 

```c++

```