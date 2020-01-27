---
title: Flood Fill
categories: leetcode
tags: DFS


---

[https://leetcode.com/submissions/detail/297843828/](https://leetcode.com/submissions/detail/297843828/){:target="_blank"}

```java
class Solution {
    int[][] image;
    int R=0,C=0;
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        this.image=image;
        R=image.length;
        C=image[0].length;
        
        paint(sr,sc,newColor, image[sr][sc]);
        return image;
    }
    
    private void paint(int sr, int sc, int newColor, int prevColor) {
        if (sr<0 || sr>=R || sc<0 || sc>=C || image[sr][sc]==newColor || image[sr][sc]!=prevColor) return;

        image[sr][sc]=newColor;
        if (sc>0) paint(sr,sc-1,newColor,prevColor);
        if (sc<C-1) paint(sr,sc+1,newColor,prevColor);
        if (sr>0) paint(sr-1,sc,newColor,prevColor);
        if (sr<R-1) paint(sr+1,sc,newColor,prevColor);
    }
}
```