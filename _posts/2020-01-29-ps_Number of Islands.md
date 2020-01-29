---
title: Number of Islands
categories: leetcode
tags: 
- DFS
- BFS
---

DFS Recursive
[https://leetcode.com/submissions/detail/298399024/](https://leetcode.com/submissions/detail/298399024/){:target="_blank"}

```java
class Solution {
    char[][] grid;
    int R=0;
    int C=0;
     
    public int numIslands(char[][] grid) {
        this.grid=grid;
        
        R=grid.length;
        if (R==0) return 0;
        C=grid[0].length;
        if (C==0) return 0;
        
        int cnt=0;
        for (int i=0;i<R;i++) {
            for (int j=0;j<C;j++) {
                if (grid[i][j]=='1') {
                    cnt+=1;
                    helper(i,j);
                }
            }
        }   
        return cnt;
    }
    
    private void helper(int i, int j) {
        if (i<0 || j<0 || i>=R || j>=C) return;
        if (grid[i][j]=='0') return;
        
        grid[i][j]='0';
        helper(i,j+1);
        helper(i,j-1);
        helper(i+1,j);
        helper(i-1,j);
    }
    
}
```

BFS iterative
[https://leetcode.com/submissions/detail/298399270/](https://leetcode.com/submissions/detail/298399270/){:target="_blank"}
```java
class Solution {
     
    public int numIslands(char[][] grid) {
        int R=grid.length;
        if (R==0) return 0;
        int C=grid[0].length;
        if (C==0) return 0;
        
        int cnt=0;
        for (int i=0;i<R;i++) {
            for (int j=0;j<C;j++) {
                if (grid[i][j]=='0') continue;
                grid[i][j]='0';
                cnt++;
                Queue<Integer> queue=new LinkedList();
                queue.add(i*C+j);
                while(!queue.isEmpty()) {
                    int val=queue.poll();
                    int r=val/C;
                    int c=val%C;
                    // System.out.println(r+"/"+c);
                    if (c+1<C && grid[r][c+1]=='1') {queue.add(r*C+(c+1)); grid[r][c+1]='0';}
                    if (c-1>=0 && grid[r][c-1]=='1') {queue.add(r*C+(c-1)); grid[r][c-1]='0';}
                    if (r+1<R && grid[r+1][c]=='1') {queue.add((r+1)*C+c); grid[r+1][c]='0';}
                    if (r-1>=0 && grid[r-1][c]=='1') {queue.add((r-1)*C+c); grid[r-1][c]='0';}
                }
            }
        }   
        return cnt;
    }
}
```
