# 1281. Subtract the Product and Sum of Digits of an Integer
**Easy**

Given an integer number n, return the difference between the product of its digits and the sum of its digits. 

```c++
class Solution {
public:
    int subtractProductAndSum(int n) {
        int p=1,s=0;
        while(n){
            int d=n%10;
            p*=d;
            s+=d;
            n/=10;
        }
        return p-s;
    }
};
```

# 1486. XOR Operation in an Array
**Easy**

You are given an integer n and an integer start.

Define an array nums where nums[i] = start + 2 * i (0-indexed) and n == nums.length.

Return the bitwise XOR of all elements of nums.

```c++
class Solution {
public:
    int xorOperation(int n, int start) {
        int ans=start, i=1;
        n--; 
        while(n--){
            ans^=(start+2*i++);
        }
        return ans;
    }
};
```

# 1688. Count of Matches in Tournament
**Easy**

You are given an integer n, the number of teams in a tournament that has strange rules:

    If the current number of teams is even, each team gets paired with another team. A total of n / 2 matches are played, and n / 2 teams advance to the next round.
    If the current number of teams is odd, one team randomly advances in the tournament, and the rest gets paired. A total of (n - 1) / 2 matches are played, and (n - 1) / 2 + 1 teams advance to the next round.

Return the number of matches played in the tournament until a winner is decided.

```c++
class Solution {
public:
    int numberOfMatches(int n) {
        int ans=0;
        while(n>1){
            ans += n&1?(n-1)/2:n/2;
            n = n&1?(n-1)/2+1:n/2;
        }
        return ans;
    }
};
```

# 1266. Minimum Time Visiting All Points
**Easy**

On a 2D plane, there are n points with integer coordinates points[i] = [xi, yi]. Return the minimum time in seconds to visit all the points in the order given by points.

You can move according to these rules:

    In 1 second, you can either:
        move vertically by one unit,
        move horizontally by one unit, or
        move diagonally sqrt(2) units (in other words, move one unit vertically then one unit horizontally in 1 second).
    You have to visit the points in the same order as they appear in the array.
    You are allowed to pass through points that appear later in the order, but these do not count as visits.


```c++
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) {
        int ans=0;
        for(auto i=1;i<points.size();i++){
            ans+=max(abs(points[i-1][0] - points[i][0]), abs(points[i-1][1] - points[i][1]));
        }
        return ans;
    }
};
```

# 268. Missing Number
Easy

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        return nums.size()*(nums.size()+1)/2 - accumulate(begin(nums), end(nums),0);
    }
};
```