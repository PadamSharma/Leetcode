# 509. Fibonacci Number
**Easy**

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.

Given n, calculate F(n).

```c++
class Solution {
public:
    // int fib(int n) { // 18ms
    //     if(n==0){
    //         return 0;
    //     }
    //     else if(n==1){
    //         return 1;
    //     }
    //     else{
    //         return fib(n-1)+fib(n-2);
    //     }
    // }
    
    int fib(int n){ // 4ms
        int a=0,b=1;
        if(n==0){
            return a;
        }
        else if(n==1){
            return b;
        }
        else{
            n-=1;
            while(n--){
                int t=b;
                b+=a;
                a=t;
            }
            return b;
        }
    }
};
```

# 1137. N-th Tribonacci Number
<!-- Easy -->

The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.

```c++
class Solution {
public:
    int tribonacci(int n) {
        int a=0,b=1,c=1;
        if(n==0){
            return a;
        }
        else if(n==1){
            return b;
        }
        else if(n==2){
            return c;
        }
        else{
            n-=2;
            while(n--){
                int t1=c,t2=b;
                c+=b+a;
                b+=a;
                a=t2;
                b=t1;
            }
            return c;
        }
    }
};
```

# 338. Counting Bits
**Easy**

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans(n+1, 0);
        if(n==0){
            return {0};
        }
        else if(n==1){
            return {0,1};
        }
        else{
            ans[1]=1;
            int i=2;
            while(i<=n){
                ans[i] = i&1?ans[i/2]+1:ans[i/2];
                i++;
            }
            return ans;
        }
        
    }
};
```

# 118. Pascal's Triangle
**Easy**

Given an integer numRows, return the first numRows of Pascal's triangle.

```c++
class Solution {
public:
    vector<vector<int>> generate(int n) {
        if(n==1){
            return {{1}};
        }
        else if(n==2){
            return {{1},{1,1}};
        }
        else{
            vector<vector<int>> ans = {{1},{1,1}};
            for(int i=3;i<=n;i++){
                vector<int> pus(i,1);
                ans.push_back(pus);
                for(int j=0;j<i-2;j++){
                    ans[i-1][j+1] = ans[i-2][j] + ans[i-2][j+1];
                }
            }
            return ans;
        }
    }
};
```