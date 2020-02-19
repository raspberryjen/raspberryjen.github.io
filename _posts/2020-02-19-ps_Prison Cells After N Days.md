---
title: Prison Cells After N Days
categories: leetcode
tags: HashTable


---

mod routine
find pattern & jump to last routine
999999999
999999998
999999997
999999996
999999995
999999994
999999993
999999992
999999991
999999990
999999989
999999988
999999987
999999986
5
4
3
2
1
0

[https://leetcode.com/submissions/detail/304690128/](https://leetcode.com/submissions/detail/304690128/){:target="_blank"}

```java
class Solution {
    public int[] prisonAfterNDays(int[] cells, int N) {
        Map<String, Integer> seen = new HashMap<>();
        while (N > 0) {
            seen.put(Arrays.toString(cells), N);
            N--;
            int[] cells2 = new int[8];
            for (int i = 1; i < 7; ++i)
                cells2[i] = cells[i - 1] == cells[i + 1] ? 1 : 0;
            cells = cells2;
            if (seen.containsKey(Arrays.toString(cells)))
                N %= seen.get(Arrays.toString(cells))-N;
        }
        return cells;
    }
}
```

Time limit
```java
class Solution {
    public int[] prisonAfterNDays(int[] cells, int N) {
        while (N > 0) {
            N--;
            int[] cells2 = new int[8];
            for (int i = 1; i < 7; ++i)
                cells2[i] = cells[i - 1] == cells[i + 1] ? 1 : 0;
            cells = cells2;
        }
        return cells;
    }
}
```
