> ### Brute Force Recursive Soln
>
> -   Time : O( 2<sup>n</sup> )
> -   Space : O( 1 ) + Auxillary Stack Space

```java
public class Solution {
    public static int frog(int ind, int[] heights)
    {
        if(ind==0){
            return 0;
        }

        int oneJump = frog(ind-1, heights) + Math.abs(heights[ind] - heights[ind-1]);

        int twoJump = Integer.MAX_VALUE;
        if(ind>=2){
            twoJump = frog(ind-2, heights) + Math.abs(heights[ind] - heights[ind-2]);
        }

        return dp[ind] = Math.min(oneJump, twoJump);

    }

    public static int frogJump(int n, int[] heights) {
        return frog(n-1, heights);
    }
}
```

<hr />

> ### Memoized Recursive Soln
>
> -   Time : O( n )
> -   Space : O( n ) + Auxillary Stack Space

```java
public class Solution {
    public static int frog(int ind, int[] heights, int[] dp)
    {
        if(ind==0){
            return 0;
        }

        if(dp[ind]!=-1){
            return dp[ind];
        }

        int oneJump = frog(ind-1, heights, dp) + Math.abs(heights[ind] - heights[ind-1]);

        int twoJump = Integer.MAX_VALUE;
        if(ind>=2)
            twoJump = frog(ind-2, heights, dp) + Math.abs(heights[ind] - heights[ind-2]);

        return dp[ind] = Math.min(oneJump, twoJump);
    }

    public static int frogJump(int n, int[] heights) {

        int[] dp = new int[n];
        for(int i=0; i<n; i++) dp[i]=-1;
        return frog(n-1, heights, dp);
    }
}
```

<hr>

> ### Tabulation
>
> -   Time : O( n )
> -   Space : O( n ) with No Auxillary Stack Space

```java
public class Solution{
    public static int frogJump(int n, int[] heights) {

        int[] dp = new int[n];
        dp[0] = 0;
        for(int ind=1; ind<n; ind++)
        {
            int oneJump = dp[ind-1] + Math.abs(heights[ind] - heights[ind-1]);

            int twoJump = Integer.MAX_VALUE;
            if(ind>=2){
                twoJump = dp[ind-2] + Math.abs(heights[ind] - heights[ind-2]);
                }
            dp[ind] = Math.min(oneJump, twoJump);
        }
        return dp[n-1];

    }
}
```
<hr>

> ### Space Optimization
>
> -   Time : O( n )
> -   Space : O( 1 )

```java
public class Solution{
    public static int frogJump(int n, int[] heights) {
        int prev = 0;
        int prev2 = 0;
        int curr=0;
        for(int i=1; i<n; i++)
        {
            int oneJump = prev + Math.abs(heights[i] - heights[i-1]);

            int twoJump = Integer.MAX_VALUE;
            if(i>=2)
                twoJump = prev2 + Math.abs(heights[i] - heights[i-2]);

            curr = Math.min(oneJump, twoJump);

            prev2 = prev;
            prev = curr;
        }
        return curr;
    }
}
```
