---
title: Count Primes
categories: leetcode

---

[https://leetcode.com/submissions/detail/296390247/](https://leetcode.com/submissions/detail/296390247/){:target="_blank"}

```java
class Solution {
    public int countPrimes(int n) {
        if (n<=2) return 0;
        boolean[] sieve = new boolean[n+1];
        sieve[2] = true;
        // for odd number
        for(int i = 3; i < n; i+=2) {
            sieve[i] = true;
        }
        
        for (int i=3;i*i<=n;i++) {
            if (!sieve[i]) continue;
            for(int j=i+i;j<n;j+=i) {
                sieve[j]=false;
            }
        }
        
        int cnt=1; // for 2
        // in odd numbers
        for (int i=3;i<n;i+=2) {
            if (sieve[i]) cnt++;
        }
        return cnt;
    }
}
```
