# 1929. Concatenation of Array
Easy

Given an integer array nums of length n, you want to create an array ans of length 2n where ans[i] == nums[i] and ans[i + n] == nums[i] for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

```c++
class Solution {
public:
    vector<int> getConcatenation(vector<int>& nums) {
        int n = nums.size();
        for(int i=0;i<n;i++){
            nums.push_back(nums[i]);
        }
        return nums;
    }
};
```

# 1480. Running Sum of 1d Array
Easy

Given an array nums. We define a running sum of an array as runningSum[i] = sum(nums[0]…nums[i]).

Return the running sum of nums.

```c++
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        for(int i=0;i<nums.size()-1;i++){
            nums[i+1]+=nums[i];
        }
        return nums;
    }
};
```

# 2011. Final Value of Variable After Performing Operations
Easy

There is a programming language with only four operations and one variable X:

    ++X and X++ increments the value of the variable X by 1.
    --X and X-- decrements the value of the variable X by 1.

Initially, the value of X is 0.

Given an array of strings operations containing a list of operations, return the final value of X after performing all the operations.

```c++
class Solution {
public:
    int finalValueAfterOperations(vector<string>& operations) {
        unordered_map<string, int> mp;
        mp["++X"]=mp["X++"]=1;
        mp["--X"]=mp["X--"]=-1;
        int ans=0;
        for(auto i:operations){
            ans+=mp[i];
        }
        return ans;
    }
};
```

# 1672. Richest Customer Wealth
Easy

You are given an m x n integer grid accounts where accounts[i][j] is the amount of money the i​​​​​​​​​​​th​​​​ customer has in the j​​​​​​​​​​​th​​​​ bank. Return the wealth that the richest customer has.

A customer's wealth is the amount of money they have in all their bank accounts. The richest customer is the customer that has the maximum wealth.

```c++
class Solution {
public:
    int maximumWealth(vector<vector<int>>& accounts) {
        int mx=0;
        for(auto i:accounts){
            mx = max(mx, accumulate(begin(i), end(i), 0));
        }
        return mx;
    }
};
```

# 2114. Maximum Number of Words Found in Sentences
Easy

A sentence is a list of words that are separated by a single space with no leading or trailing spaces.

You are given an array of strings sentences, where each sentences[i] represents a single sentence.

Return the maximum number of words that appear in a single sentence.

```c++
class Solution {
public:
    int mostWordsFound(vector<string>& sen) {
        int ans=0;
        for(auto i:sen){
            int w=0;
            i+=' ';
            for(auto j:i){
                if(j==' '){
                    w++;
                }
            }
            ans = max(ans, w);
        }
        return ans;
    }
};
```

# 1470. Shuffle the Array
Easy

Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

Return the array in the form [x1,y1,x2,y2,...,xn,yn].

```c++
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> ans;
        for(int i=0,j=n;i<n,j<2*n;i++,j++){
            ans.push_back(nums[i]);
            ans.push_back(nums[j]);
        }
        return ans;
    }
};
```

# 1431. Kids With the Greatest Number of Candies
Easy

There are n kids with candies. You are given an integer array candies, where each candies[i] represents the number of candies the ith kid has, and an integer extraCandies, denoting the number of extra candies that you have.

Return a boolean array result of length n, where result[i] is true if, after giving the ith kid all the extraCandies, they will have the greatest number of candies among all the kids, or false otherwise.

Note that multiple kids can have the greatest number of candies.

```c++
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
        int mx = *max_element(begin(candies), end(candies));
        vector<bool> ans;
        for(auto i:candies){
            ans.push_back(i+extraCandies>=mx);
        }
        return ans;
    }
};
```