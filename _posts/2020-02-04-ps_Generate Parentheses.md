---
title: Generate Parentheses
categories: leetcode
tags:
- Backtracking
- more

---

https://youtu.be/Bt11jaoqt_Y
backtracking = recursion + termiation check

[](){:target="_blank"}

```java
class Solution {
    List<String> ans=new ArrayList();
    int N=0;
    private void generate(int openCnt, int closeCnt, String str) {
        if (openCnt==N && closeCnt==N) {
            ans.add(str);
            return;
        }
        if (openCnt<N)
            generate(openCnt+1, closeCnt, str+"(");
        if (openCnt>closeCnt)
            generate(openCnt, closeCnt+1, str+")");
    }
    
    public List<String> generateParenthesis(int n) {
        this.N=n;
        generate(0, 0, "");
        
        return ans;
    }
    
}
```
