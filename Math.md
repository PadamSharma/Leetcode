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