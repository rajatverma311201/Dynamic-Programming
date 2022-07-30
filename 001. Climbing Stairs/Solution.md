# Climbing Stairs

## [Leetcode Problem Link](https://leetcode.com/problems/climbing-stairs/)

> ### Brute Force Approach
>
> -   Time : O( 2<sup>n</sup> )
> -   Space : O( 1 ) + Auxillary Stack Space

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
> -   Time : O( n )
> -   Space: O( n ) + Auxillary Stack Space

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
> -   Time : O( n )
> -   Space : O( n ) and No Auxillary Stack Space

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
