# 1512. Number of Good Pairs
**Easy**

`Given an array of integers nums, return the number of good pairs.
A pair (i, j) is called good if nums[i] == nums[j] and i < j.`

> Update ans (no. of pairs) as how many other same elements are there already in the map, leaving out itself. This would be no. of pairs that it can form.


```c++
class Solution {
public:
    int numIdenticalPairs(vector<int>& nums) {
        unordered_map<int,int> m;
        int ans=0;
        for(auto i:nums){
            m[i]++;
            if(m[i]>1) ans+=(m[i]-1);
        }
        return ans;
    }
};
```

# 771. Jewels and Stones
**Easy**

`You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels.
Letters are case sensitive, so "a" is considered a different type of stone from "A".`

> Update no. of same chars by incrementing no. of same chars as they occur in map.

```c++
class Solution {
public:
    int numJewelsInStones(string jewels, string stones) {
        unordered_map<char,int> m;
        int ans=0;
        for(auto i:stones){
            m[i]++;
        }
        for(auto i:jewels){
            if(m[i]>=1) ans+=(m[i]);
        }
        return ans;
    }
};
```

# 1365. How Many Numbers Are Smaller Than the Current Number
**Easy**

`Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].
Return the answer in an array.`

> Ordered map keeps sorted order of keys so iterate over the map and update count there only and then return the count in the specified order.

```c++
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        map<int,int> map;
        for(auto i:nums){
            map[i]++;
        }
        int c=0;
        for(auto& i:map){
            int temp = i.second;
            i.second = c;
            c += temp;
        }
        for(auto& i:nums){
            i = map[i];
        }
        return nums;
    }
};
```

# 2006. Count Number of Pairs With Absolute Difference K
**Easy**

`Given an integer array nums and an integer k, return the number of pairs (i, j) where i < j such that |nums[i] - nums[j]| == k.
The value of |x| is defined as:
    x if x >= 0.
    -x if x < 0.`

> Important point is to frame unique pairs. Checking and updating the map at the same time, benefits us as elements can only see their predeccessor elements and not their successor. Hence they form unique pairs.

```c++
class Solution {
public:
    int countKDifference(vector<int>& nums, int k) {
        map<int,int> map;
        int ans=0;
        for(auto i:nums){
            if(map[i+k]) ans+=map[i+k];
            if(map[i-k]) ans+=map[i-k];
            map[i]++;
        }
        return ans;
    }
};
```

# 1684. Count the Number of Consistent Strings
**Easy**

`You are given a string allowed consisting of distinct characters and an array of strings words. A string is consistent if all characters in the string appear in the string allowed.
Return the number of consistent strings in the array words.`

> Create map of str 'allowed' and iterate over the words to check if all chars are in the map, if not break loop of that word and decrement ans.

```c++
class Solution {
public:
    int countConsistentStrings(string allowed, vector<string>& words) {
        int ans=words.size();
        unordered_map<char,int> map;
        for(auto i:allowed){
            map[i]++;
        }
        for(auto i:words){
            for(auto c:i){
                if(!map[c]){
                    ans--;
                    break;
                }
            }
            
        }
        return ans;
    }
};
```

# 2103. Rings and Rods
**Easy**

`There are n rings and each ring is either red, green, or blue. The rings are distributed across ten rods labeled from 0 to 9.
You are given a string rings of length 2n that describes the n rings that are placed onto the rods. Every two characters in rings forms a color-position pair that is used to describe each ring where:
    The first character of the ith pair denotes the ith ring's color ('R', 'G', 'B').
    The second character of the ith pair denotes the rod that the ith ring is placed on ('0' to '9').
For example, "R3G2B1" describes n == 3 rings: a red ring placed onto the rod labeled 3, a green ring placed onto the rod labeled 2, and a blue ring placed onto the rod labeled 1.
Return the number of rods that have all three colors of rings on them.`

> Make 3 maps for RGB, and check if R>0, G>0, B>0.

```c++
class Solution {
public:
    int countPoints(string rings) {
        int r[11] = {}, g[11] = {}, b[11] = {};
        for(int i=0;i<rings.length()-1;i+=2){
            if(rings[i]=='R'){
                r[rings[i+1]-48]++;
            }
            else if(rings[i]=='G'){
                g[rings[i+1]-48]++;
            }
            else if(rings[i]=='B'){
                b[rings[i+1]-48]++;
            }
        }
        int ans=0;
        for(int i=0;i<10;i++){
            if(r[i]>0 && g[i]>0 && b[i]>0){
                ans++;
            }
        }
        return ans;
    }
};
```

# 1832. Check if the Sentence Is Pangram
**Easy**

`A pangram is a sentence where every letter of the English alphabet appears at least once.
Given a string sentence containing only lowercase English letters, return true if sentence is a pangram, or false otherwise.`

```c++
class Solution {
public:
    bool checkIfPangram(string sentence) {
        int map[26]={};
        for(auto i:sentence){
            map[i-97]++;
        }
        for(int i=0;i<26;i++){
            if(map[i]==0){
                return false;
            }
        }
        return true;
    }
};
```

# 804. Unique Morse Code Words
**Easy**

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows:

    'a' maps to ".-",
    'b' maps to "-...",
    'c' maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:

[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]

Given an array of strings words where each word can be written as a concatenation of the Morse code of each letter.

    For example, "cab" can be written as "-.-..--...", which is the concatenation of "-.-.", ".-", and "-...". We will call such a concatenation the transformation of a word.

Return the number of different transformations among all words we have.

> Create map of morse code and then gen string, create another map of string and iterate over map to see unique codes.

```c++
class Solution {
public:
    int uniqueMorseRepresentations(vector<string>& words) {
        vector<string> s = {".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
        unordered_map<string, int> map;
        for(auto i:words){
            string str="";
            for(auto c:i){
                str+=s[c-97];
            }
            map[str]++;
        }
        int ans=0;
        for(auto i:map){
            ans++;
        }
        return ans;
    }
};
```

# 1436. Destination City
**Easy**

You are given the array paths, where paths[i] = [cityAi, cityBi] means there exists a direct path going from cityAi to cityBi. Return the destination city, that is, the city without any path outgoing to another city.

It is guaranteed that the graph of paths forms a line without any loop, therefore, there will be exactly one destination city.

```c++
class Solution {
public:
    string destCity(vector<vector<string>>& paths) {
        unordered_map<string, int> map;
        for(auto i:paths){
            map[i[0]]++;
        }
        string ans="";
        for(auto i:paths){
            if(!map[i[1]]){
                ans = i[1];
                break;
            }
        }
        return ans;
    }
};
```

# 1941. Check if All Characters Have Equal Number of Occurrences
**Easy**

Given a string s, return true if s is a good string, or false otherwise.

A string s is good if all the characters that appear in s have the same number of occurrences (i.e., the same frequency).

```c++
class Solution {
public:
    bool areOccurrencesEqual(string s) {
        unordered_map<int, int> map;
        for(auto i:s){
            map[i]++;
        }
        int ans = map.begin()->second;
        for(auto i:map){
            if(i.second != ans){
                return false;
            }
        }
        return true;
    }
};
```

# 2206. Divide Array Into Equal Pairs
**Easy**

You are given an integer array nums consisting of 2 * n integers.

You need to divide nums into n pairs such that:

    Each element belongs to exactly one pair.
    The elements present in a pair are equal.

Return true if nums can be divided into n pairs, otherwise return false.

```c++
class Solution {
public:
    bool divideArray(vector<int>& nums) {
        unordered_map<int,int> map;
        for(auto i:nums){
            map[i]++;
        }
        for(auto i:map){
            if(i.second % 2){
                return false;
            }
        }
        return true;
    }
};
```

# 1748. Sum of Unique Elements
**Easy**

You are given an integer array nums. The unique elements of an array are the elements that appear exactly once in the array.

Return the sum of all the unique elements of nums.

```c++
class Solution {
public:
    int sumOfUnique(vector<int>& nums) {
        unordered_map<int ,int> map;
        for(auto i:nums){
            map[i]++;
        }
        int ans=0;
        for(auto i:map){
            if(i.second == 1){
                ans+=i.first;
            }
        }
        return ans;
    }
};
```

# 961. N-Repeated Element in Size 2N Array
**Easy**

You are given an integer array nums with the following properties:

    nums.length == 2 * n.
    nums contains n + 1 unique elements.
    Exactly one element of nums is repeated n times.

Return the element that is repeated n times.

```c++
class Solution {
public:
    int repeatedNTimes(vector<int>& nums) {
        unordered_map<int,int> map;
        int ans=0;
        for(auto i:nums){
            if(map[i]){
                ans = i;
                break;
            }
            map[i]++;
        }
        return ans;
    }
};
```

# 1742. Maximum Number of Balls in a Box
**Easy**

You are working in a ball factory where you have n balls numbered from lowLimit up to highLimit inclusive (i.e., n == highLimit - lowLimit + 1), and an infinite number of boxes numbered from 1 to infinity.

Your job at this factory is to put each ball in the box with a number equal to the sum of digits of the ball's number. For example, the ball number 321 will be put in the box number 3 + 2 + 1 = 6 and the ball number 10 will be put in the box number 1 + 0 = 1.

Given two integers lowLimit and highLimit, return the number of balls in the box with the most balls.

```c++
class Solution {
public:
    int countBalls(int lowLimit, int highLimit) {
        unordered_map<int, int> m;
        for(int i=lowLimit;i<=highLimit;i++){
            int n=i,s=0;
            while(n){
                int d=n%10;
                s+=d;
                n/=10;
            }
            m[s]++;
        }
        int ans=0;
        for(auto i:m){
            ans = max(ans, i.second);
        }
        return ans;
    }
};
```

# 2032. Two Out of Three
**Easy**

Given three integer arrays nums1, nums2, and nums3, return a distinct array containing all the values that are present in at least two out of the three arrays. You may return the values in any order. 

> Used 3 sets for 3 arrays and calculated frequency of the elements in all 3 sets. The elements with freq > 2 are pushed in ans.

> Main thing is how to return the vector from vector of vectors and make sets.

```c++
class Solution {
public:
    vector<int> twoOutOfThree(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3) {
        unordered_map<int, int> freq; 
        for (auto& nums : {nums1, nums2, nums3}) {
            unordered_set<int> st(nums.begin(), nums.end()); 
            for (auto& x : st) ++freq[x];
        }
        vector<int> ans; 
        for (auto& [k, v] : freq)
            if (v >= 2) ans.push_back(k); 
        return ans;
    }
};
```

# 2053. Kth Distinct String in an Array
**Easy**

A distinct string is a string that is present only once in an array.

Given an array of strings arr, and an integer k, return the kth distinct string present in arr. If there are fewer than k distinct strings, return an empty string "".

Note that the strings are considered in the order in which they appear in the array.

> Order if based on the array and kth element is found using --k == 0.

```c++
class Solution {
public:
    string kthDistinct(vector<string>& arr, int k) {
        unordered_map<string, int> map;
        for(auto i:arr){
            map[i]++;
        }
        string ans;
        for(auto i:arr){
            if(map[i]==1 && --k == 0){
                ans = i;
                break;
            }
        }
        return ans;
    }
};
```

# 1460. Make Two Arrays Equal by Reversing Sub-arrays
**Easy**

You are given two integer arrays of equal length target and arr. In one step, you can select any non-empty sub-array of arr and reverse it. You are allowed to make any number of steps.

Return true if you can make arr equal to target or false otherwise.

```c++
class Solution {
public:
    bool canBeEqual(vector<int>& target, vector<int>& arr) {
        unordered_map<int,int> map;
        if(target.size()!=arr.size()){
            return false;
        }
        for(int i=0;i<arr.size();i++){
            map[arr[i]]++;
            map[target[i]]--;
        }
        for(auto i:map){
            if(i.second!=0){
                return false;
            }
        }
        return true;
    }
};
```

# 1207. Unique Number of Occurrences
**Easy**

Given an array of integers arr, return true if the number of occurrences of each value in the array is unique, or false otherwise.

```c++
class Solution {
public:
    bool uniqueOccurrences(vector<int>& arr) {
        unordered_map<int,int> map;
        for(auto i:arr){
            map[i]++;
        }
        unordered_set<int> s;
        for(auto i:map){
            s.insert(i.second);
        }
        return s.size()==map.size();
    }
};
```

# 

```c++

```