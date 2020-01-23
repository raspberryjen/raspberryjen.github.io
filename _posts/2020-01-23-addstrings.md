---
title: Add Strings
categories: leetcode
---

char -> int
num1.charAt(i--)-'0'


```java
class Solution {
    public String addStrings(String num1, String num2) {
        StringBuilder ans=new StringBuilder();
        int n1=0,n2=0,sum=0,carry=0;
        int i=num1.length()-1,j=num2.length()-1;
        while(i>=0 || j>=0 || carry>0) {
            n1= (i<0) ? 0 : num1.charAt(i--)-'0';
            n2= (j<0) ? 0 : num2.charAt(j--)-'0';
            sum=n1+n2+carry;
            carry=sum/10;
            ans.append(sum%10);
        }
        
        return ans.reverse().toString();
    }
}
```
