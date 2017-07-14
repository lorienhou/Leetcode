Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
Thoughts: Obviously dp.
I know that n = something1 + i*i. This means that dp[n] = something2 + 1 and something2 = Min(dp[n - i*i]), we just need to try every i such that n - i*i >= 0
```java
public class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n+1];
        dp[0] = 0;
        for (int i=1; i<=n; i++) {// we're going to use the recursive formula for each i
        int min = Integer.MAX_VALUE;
            for (int j=1; i-j*j>=0; j++) {//we're sure that all dp[x] where x<i have been filled
                if (dp[i-j*j] < min)
                    min = dp[i-j*j];
            }
            dp[i] = min + 1;
        }
        return dp[n];
    }
}
```
