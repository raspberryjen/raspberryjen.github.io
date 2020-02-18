---
title: Design Tic-Tac-Toe
categories: leetcode
tags: design

---

[](){:target="_blank"}

```java
class TicTacToe {
    int[] rows;
    int[] cols;
    int diagonal=0;
    int anti_diagonal=0;
    int N=0;
    
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        if (n<=0) return;
        N=n;
        // each row sum as player offset
        // row[0] 1 1 -1 => if row complete should be 3 or -3
        rows=new int[N];
        cols=new int[N];
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        int offset=player==1? 1:-1;
        int sum=offset*N;
        rows[row]+=offset;
        cols[col]+=offset;
        if (row==col) diagonal+=offset;
        if (row==N-1-col) anti_diagonal+=offset;
        if (rows[row]==sum || cols[col]==sum || diagonal==sum || anti_diagonal==sum)
            return player;
        else
            return 0;
    }
    
}

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
```


```java
class TicTacToe {
    int[][] board;
        
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        if (n>0)
            board=new int[n][n];
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        board[row][col]=player;
        return isComplete(row,col,player)? player:0;
    }
    
    private boolean isComplete(int row,int col,int player) {
        int i=0;
        for (i=0;i<board.length;i++) {
            if (board[row][i]!=player)
                break;
        }

        if (i==board.length) return true;
        
        for (i=0;i<board.length;i++){
            if (board[i][col]!=player)
                break;
        }
        if (i==board.length) return true;
        
        for (i=0;i<board.length;i++) {
            if (board[i][i]!=player)
                break;
        }
        if (i==board.length) return true;
        
        int j=0;
        for (i=0,j=board.length-1;i<board.length;i++,j--) {
            if (board[i][j]!=player)
                break;
        }
        if (i==board.length) return true;
        return false;
    }
}

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
 ```
