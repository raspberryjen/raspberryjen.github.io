---
title: Decode String
categories: leetcode
tags: DFS


---

394. Decode String
[https://leetcode.com/submissions/detail/298626078/](https://leetcode.com/submissions/detail/298626078/){:target="_blank"}

```java
class Solution {
    private String helper(int cnt, String s) {
        if (s.isEmpty()) return "";
        
        StringBuilder sb=new StringBuilder();
        int i=0;
        int subCnt=0;
        int bracket=0;
        StringBuilder sub=new StringBuilder();
        StringBuilder digitSb=new StringBuilder();
        while (i<s.length()) {
            char ch=s.charAt(i);
            if (bracket==0) {
                if (Character.isDigit(ch)) {
                    digitSb.append(ch);
                } else if (ch=='[') {
                    subCnt=Integer.parseInt(digitSb.toString());
                    digitSb.setLength(0);
                    bracket++;
                } else {
                    sb.append(ch);
                }
            } else {
                if (ch==']') {
                    bracket--;
                    if (bracket==0) {
                        sb.append(helper(subCnt, sub.toString()));
                        subCnt=0;
                        sub.setLength(0);
                    } else {
                        sub.append(ch);
                    }
                } else if (ch=='[') {
                    bracket++;
                    sub.append(ch);
                } else {
                    sub.append(ch);
                }
            }
            i++;
        }
        
        String ans=sb.toString();
        for (int j=0;j<cnt-1;j++)
            sb.append(ans);
        return sb.toString();
    }
    
    public String decodeString(String s) {
        if (s.isEmpty()) return s;
        return helper(1,s);
    }
    
}
```
