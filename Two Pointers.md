# 832. Flipping an Image
**Easy**

Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.

For example, flipping [1,1,0] horizontally results in [0,1,1].
To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0.

For example, inverting [0,1,1] results in [1,0,0].

```c++
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& image) {
        for(auto& v:image){
            int i=0,j=v.size()-1;
            while(i<=j){
                int temp = v[i];
                v[i] = !v[j];
                v[j] = !temp;
                i++;
                j--;
            }
        }
        return image;
    }
};
```

# 2108. Find First Palindromic String in the Array
**Easy**

Given an array of strings words, return the first palindromic string in the array. If there is no such string, return an empty string "".

A string is palindromic if it reads the same forward and backward.

```c++
class Solution {
public:
    string firstPalindrome(vector<string>& words) {
        string ans="";
        for(auto w:words){
            int i=0,j=w.length()-1;
            int c=0;
            while(i<=j){
                if(w[i]==w[j]){
                    c++;
                }
                else{
                    break;
                }
                i++;
                j--;
            }
            cout<<c<<endl;
            if(c==int((w.length()+1)/2)){
                ans=w;
                break;
            }
        }
        return ans;
    }
};
```

# 557. Reverse Words in a String III
**Easy**

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        w = s.split(' ')
        ans = ""
        for i in w:
            ans+=i[::-1]+" "
        return ans[:-1]
```

# 2000. Reverse Prefix of Word
**Easy**

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

For example, if word = "abcdefd" and ch = "d", then you should reverse the segment that starts at 0 and ends at 3 (inclusive). The resulting string will be "dcbaefd".
Return the resulting string.

```c++
class Solution {
public:
    string reversePrefix(string word, char ch) {
        int i=0;
        for(auto c:word){
            if(c==ch){
                break;
            }
            i++;
        }
        if(i<word.length()){
            reverse(word.begin(), word.begin()+i+1);
        }
        return word;
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
        vector<int> n(s.length()+1, 0);
        int i=0,d=s.length();
        for(int j=0;j<s.length();j++){
            if(s[j] == 'I'){
                n[j]=i;
                i++;
            }
            else{
                n[j]=d;
                d--;
            }
        }
        if(s[s.length()-1]=='I'){
            n[s.length()] = d;
        }
        else{
            n[s.length()] = i;
        }
        return n;
    }
};
```

