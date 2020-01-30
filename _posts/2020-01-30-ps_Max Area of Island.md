---
title: Max Area of Island
categories: leetcode
tags:
- DFS
- BFS

---

DFS
Recursive
[https://leetcode.com/submissions/detail/298645073/](https://leetcode.com/submissions/detail/298645073/){:target="_blank"}
```java
class Solution {
    int[][] grid;
    int R=0;
    int C=0;
    private int helper(int r,int c){
        if (r<0 || c<0 || r>=R || c>=C)
            return 0;
        if (grid[r][c]==0) return 0 ;
        int area=0;
        grid[r][c]=0;
        area+=helper(r, c+1);
        area+=helper(r, c-1);
        area+=helper(r+1, c);
        area+=helper(r-1, c);
        return area+1;
    }
    
    public int maxAreaOfIsland(int[][] grid) {
        this.grid=grid;
        
        R=grid.length;
        if (R==0) return 0;
        C=grid[0].length;
        if (C==0) return 0;

        int max=0;
        for (int i=0;i<R;i++) {
            for (int j=0;j<C;j++) {
                if (grid[i][j]==1) {
                    max=Math.max(max, helper(i, j));
                }
            }
        }
        return max; 
    }
}
```

BFS
Iterative
```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int R=grid.length;
        if (R==0) return 0;
        int C=grid[0].length;
        if (C==0) return 0;

        int max=0;
        int area=0;
        Queue<Integer> q=new LinkedList();
        for (int i=0;i<R;i++) {
            for (int j=0;j<C;j++) {
                if (grid[i][j]==0) continue; 
                grid[i][j]=0;
                area=1;
                q.add(i*C+j);
                while(!q.isEmpty()) {
                    int num=q.poll();
                    int r=num/C;
                    int c=num%C;
                    if (c+1<C && grid[r][c+1]==1) {
                        grid[r][c+1]=0;
                        area++;
                        q.add(r*C+(c+1));
                    }
                    if (c-1>=0 && grid[r][c-1]==1) {
                        grid[r][c-1]=0;
                        area++;
                        q.add(r*C+(c-1));
                    }
                    if (r+1<R && grid[r+1][c]==1) {
                        grid[r+1][c]=0;
                        area++;
                        q.add((r+1)*C+c);
                    }
                    if (r-1>=0 && grid[r-1][c]==1) {
                        grid[r-1][c]=0;
                        area++;
                        q.add((r-1)*C+c);
                    }
                }
                max=Math.max(max, area);
            }
        }
        return max;
    }
}
```



