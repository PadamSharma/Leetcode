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

# 1313. Decompress Run-Length Encoded List
Easy

We are given a list nums of integers representing a list compressed with run-length encoding.

Consider each adjacent pair of elements [freq, val] = [nums[2*i], nums[2*i+1]] (with i >= 0).  For each such pair, there are freq elements with value val concatenated in a sublist. Concatenate all the sublists from left to right to generate the decompressed list.

Return the decompressed list.

```c++
class Solution {
public:
    vector<int> decompressRLElist(vector<int>& nums) {
        vector<int> ans;
        for(int i=0;i<nums.size();i+=2){
            while(nums[i]--){
                ans.push_back(nums[i+1]);
            }
        }
        return ans;
    }
};
```

# 1528. Shuffle String
Easy

You are given a string s and an integer array indices of the same length. The string s will be shuffled such that the character at the ith position moves to indices[i] in the shuffled string.

Return the shuffled string.

> # Cycle Sort - TODO

```c++
class Solution {
public:
    string restoreString(string s, vector<int>& indices) {
        for(auto i=0;i<indices.size();i++){
            while(indices[i]!=i){
                swap(s[i], s[indices[i]]);
                swap(indices[i], indices[indices[i]]);
            }
        }
        return s;
    }
};
```

# 1773. Count Items Matching a Rule
Easy

You are given an array items, where each items[i] = [typei, colori, namei] describes the type, color, and name of the ith item. You are also given a rule represented by two strings, ruleKey and ruleValue.

The ith item is said to match the rule if one of the following is true:

    ruleKey == "type" and ruleValue == typei.
    ruleKey == "color" and ruleValue == colori.
    ruleKey == "name" and ruleValue == namei.

Return the number of items that match the given rule.

```c++
class Solution {
public:
    int countMatches(vector<vector<string>>& items, string ruleKey, string ruleValue) {
        unordered_map<string, int> mp;
        mp["type"]=0;
        mp["color"]=1;
        mp["name"]=2;
        int ans=0;
        for(auto i:items){
            if(i[mp[ruleKey]]==ruleValue){
                ans++;
            }
        }
        return ans;
    }
};
```

# 

```c++

```