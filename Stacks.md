# 1614. Maximum Nesting Depth of the Parentheses
**Easy**

A string is a valid parentheses string (denoted VPS) if it meets one of the following:

    It is an empty string "", or a single character not equal to "(" or ")",
    It can be written as AB (A concatenated with B), where A and B are VPS's, or
    It can be written as (A), where A is a VPS.

We can similarly define the nesting depth depth(S) of any VPS S as follows:

    depth("") = 0
    depth(C) = 0, where C is a string with a single character not equal to "(" or ")".
    depth(A + B) = max(depth(A), depth(B)), where A and B are VPS's.
    depth("(" + A + ")") = 1 + depth(A), where A is a VPS.

For example, "", "()()", and "()(()())" are VPS's (with nesting depths 0, 1, and 2), and ")(" and "(()" are not VPS's.

Given a VPS represented as string s, return the nesting depth of s.

```c++
class Solution {
public:
    int maxDepth(string s) {
        int ans=0, c=0;
        for(auto i:s){
            if(i=='('){
                c++;
                ans = max(ans,c);
            }
            else if(i==')'){
                c--;
            }
        }
        return ans;
    }
};
```

# 1021. Remove Outermost Parentheses
Easy

A valid parentheses string is either empty "", "(" + A + ")", or A + B, where A and B are valid parentheses strings, and + represents string concatenation.

    For example, "", "()", "(())()", and "(()(()))" are all valid parentheses strings.

A valid parentheses string s is primitive if it is nonempty, and there does not exist a way to split it into s = A + B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string s, consider its primitive decomposition: s = P1 + P2 + ... + Pk, where Pi are primitive valid parentheses strings.

Return s after removing the outermost parentheses of every primitive string in the primitive decomposition of s.

> Primitve parantheses have same number of closing and opening parentheses. Thus maintaining a current count of parentheses can help to identify the primitive substring as count = 0.

> Now if current parentheses is '(' and count = 0, primitive parentheses starts thus start to append next parentheses into ans, else if current parentheses is ')' and count = 2, and in next iteration it becomes 0(pre-decrement operator is used), then primitive subtsring ends, so do not append that last character for which count = 1, into ans as it is not the part of the primitive substring.

```c++
class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans="";
        int cnt = 0;
        for(auto i:s){
            if(i=='(' && ++cnt > 1){
                ans+=i;
            }
            else if(i==')' && --cnt >= 1){
                ans+=i;
            }
        }
        return ans;
    }
};
```

# 1475. Final Prices With a Special Discount in a Shop
**Easy**

Given the array prices where prices[i] is the price of the ith item in a shop. There is a special discount for items in the shop, if you buy the ith item, then you will receive a discount equivalent to prices[j] where j is the minimum index such that j > i and prices[j] <= prices[i], otherwise, you will not receive any discount at all.

Return an array where the ith element is the final price you will pay for the ith item of the shop considering the special discount.

```c++
class Solution {
public:
    vector<int> finalPrices(vector<int>& prices) {
        stack<int> s;
        // Iterate over the prices array
        for(int i=0;i<prices.size();i++){
            // Iterate over the stack until the stack is not empty and the current element is less than the element at the top of the stack, then pop the top of the stack
            while(!s.empty() && prices[s.top()]>=prices[i]){
                prices[s.top()]-=prices[i];
                s.pop();
            }
            // Push the current index into the stack
            s.push(i);
        }
        return prices;
    }
};
```

