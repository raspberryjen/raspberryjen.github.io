---
title: Generate Parentheses
categories: leetcode
tags:
- Backtracking
- more

---

[](){:target="_blank"}

```java
class Solution {
    List<String> ans=new ArrayList();
    int N=0;
    private void generate(int left, int right, String str) {
        if (left==N && right==N) {
            ans.add(str);
            return;
        }
        if (left<N)
            generate(left+1, right, str+"(");
        if (left>right)
            generate(left, right+1, str+")");
    }
    
    public List<String> generateParenthesis(int n) {
        this.N=n;
        generate(0, 0, "");
        
        return ans;
    }
    
}
```
