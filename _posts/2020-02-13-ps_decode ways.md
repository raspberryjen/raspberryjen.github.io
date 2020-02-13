---
title: Decode Ways
categories: leetcode
tags: DP


---

[](){:target="_blank"}

```java
class Solution {
    public int numDecodings(String s) {
        if (s.isEmpty()) return 0;
        int one=0,two=0;
        int dp[]=new int[s.length()+1];
        Arrays.fill(dp, 0);
        dp[0]=1;            // empty string
        dp[1]=s.charAt(0)<='9' && s.charAt(0)>='1'? 1:0;    // length 1 string
        for (int i=2;i<=s.length();i++) {
            one=Integer.parseInt(s.substring(i-1,i));
            two=Integer.parseInt(s.substring(i-2,i));
            if (one>=1 && one<=9) dp[i]=dp[i-1];
            if (two>=10 && two<=26) dp[i]+=dp[i-2];
        }
        return dp[s.length()];
    }
}
```

알파벳이 될 가능성이 있는 수는 한자리 수(1~9)이거나 두 자리 수(10~26)다.
문자열을 앞에서부터 탐색하면서 한자리 수와 현재 탐색중인 문자보다 하나 작은 문자를 합쳐서 두 자리 수를 구해 이들이 알파벳이 될 수 있는지 체크한다. ex) "12" -> 1, 2, 12 체크.
탐색 중인 문자열 인덱스를 ind라 하고 
ind번째 문자열까지 만들 수 있는 알파벳문자열의 경우의 수를 저장하는 d[ind] 배열을 만든다.
한 자리 수가 숫자가 될 수 있는 경우 ind-1 번째 문자열까지 만들 수 있는 알파벳 배열의 수(d[ind-1])를 d[ind]에 더한다. (d[ind-1]로 만들 수 있는 알파벳 문자열 뒤에 알파벳 하나만 붙이면 d[ind]에 저장될 수 있는 알파벳 문자열이 되므로. ex) A -> AB : A뒤에 B하나를 붙임. 경우의 수는 똑같이 1임.)

두 자리 수가 숫자가 될 수 있는 경우 ind-2 번재 문자열까지 만들 수 있는 알파벳 배열의 수(d[ind-2])를 d[ind]에 더한다. (d[ind-2]로 만들 수 있는 알파벳 문자열 뒤에 알파벳 하나만 붙이면 d[ind]에 저장될 수 있는 알파벳 문자열이 되므로.)
만약 ind-1, ind-2가 배열의 범위를 벗어난다면 1을 더하면 된다. ex) "12" -> d[0] = 1("1"), d[2] = 2("12", "2")
입력 문자열 길이를 입력 문자열 길이만큼 만들었지만 사실 참조하는 범위는 현재보다 2작은 것(ind-2)까지만 참조하므로 3 크기의 배열만 만들어도 풀 수 있다.
시간복잡도는 O(|s|).
