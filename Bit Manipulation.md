# 1342. Number of Steps to Reduce a Number to Zero
**Easy**

Given an integer num, return the number of steps to reduce it to zero.

In one step, if the current number is even, you have to divide it by 2, otherwise, you have to subtract 1 from it.

> Some important builtin functions for bit manipulation,

* **__builtin_clz(x)** : the number of zeros at the beginning of the bit representation
* **__builtin_ctz(x)** : the number of zeros at the end of the bit representation
* **__builtin_popcount(x)** : the number of ones in the bit representation
* **__builtin_parity(x)** : the parity (even or odd) of the number of ones in the bit representation
* **64 - __builtin_clzl(x) - 1** : Binary logarithm of the integer

```c++
class Solution {
public:
    int numberOfSteps(int x) {
        if(x==0){
            return 0;
        }
        else
        return (64 - __builtin_clzl(x) - 1) + __builtin_popcount(x);
    }
};
```

# 1720. Decode XORed Array
Easy

There is a hidden integer array arr that consists of n non-negative integers.

It was encoded into another integer array encoded of length n - 1, such that encoded[i] = arr[i] XOR arr[i + 1]. For example, if arr = [1,0,2,1], then encoded = [1,2,3].

You are given the encoded array. You are also given an integer first, that is the first element of arr, i.e. arr[0].

Return the original array arr. It can be proved that the answer exists and is unique.

```c++
class Solution {
public:
    vector<int> decode(vector<int>& encoded, int first) {
        vector<int> ans(encoded.size()+1, first);
        for(int i=0;i<encoded.size();i++){
            ans[i+1] = encoded[i]^ans[i];
        }
        return ans;
    }
};
```

# 

```c++

```