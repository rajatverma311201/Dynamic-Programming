# Frog Jump

## [Leetcode Problem Link](https://leetcode.com/problems/climbing-stairs/)

### You are climbing a staircase. It takes n steps to reach the top.Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

```
Example 1:
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

```
Example 2:
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

Constraints:

```
1 <= n <= 45
```

> ### Brute Force Approach
>
> <code>
> Time : O(2<sup>n</sup>)</br>
> Space : O(1) + Auxillary Stack Space
> </code>

```java
   class Solution {
        public int findWays(int ind)
        {
            if(ind==0)
            {
                return 1;
            }
            if(ind<0)
            {
                return 0;
            }
            int oneStep = findWays(ind-1);
            int twoStep = findWays(ind-2);
            return oneStep + twoStep;
        }

        public int climbStairs(int n) {
            return findWays(n);
        }
    }
```

<hr>

> ### Memoized Recursion Approach
>
> <code> 
> Time : O(n) <br>
> Space: O(n) + Auxillary Stack Space
> </code>

```java
    class Solution {
        public int findWays(int ind, int[] dp)
        {
            if(ind==0)
            {
                return 1;
            }
            if(ind<0)
            {
                return 0;
            }

            if(dp[ind]!=-1) return dp[ind];

            int oneStep = findWays(ind-1, dp);
            int twoStep = findWays(ind-2, dp);

            return dp[ind] = oneStep + twoStep;
        }

        public int climbStairs(int n) {
            int[] dp = new int[n+1];
            Arrays.fill(dp, -1);

            return findWays(n, dp);
        }
    }
```

<hr>

> ### Most Optimized Iterative Soln
>
> <code>
> Time : O(n) <br>
> Space : O(n) and No Auxillary Stack Space
> </code>

```java
class Solution {

    public int findWays(int n)
    {
        if(n==0)
        {
            return 1;
        }
        if(n==1)
        {
            return 1;
        }

        int t = 0;
        int t1 = 1, t2=1;

        for(int i=2; i<=n; i++)
        {
            t = t1+t2;
            t1 = t2;
            t2 = t;
        }
        return t;
    }
    public int climbStairs(int n) {
        return findWays(n);
    }
}
```

<hr>
