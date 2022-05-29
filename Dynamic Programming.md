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