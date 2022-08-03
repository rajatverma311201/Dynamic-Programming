> ### Memoized Recursion Solution
>
> -   Time : O( n )
> -   Space : O( n ) and Auxillary Stack Space

```java
class Solution {

    public int find(int ind, int[] arr, int[] dp)
    {
        if(ind==0)
        {
            return arr[ind];
        }
        if(ind<0)
        {
            return 0;
        }
        if(dp[ind]!=-1)
        {
            return dp[ind];
        }
        // take the current element
        int take = arr[ind] + find(ind-2, arr, dp);

        // don't take the current element
        int notTake = 0 + find(ind-1, arr, dp);

        return dp[ind] = Math.max(take, notTake);
    }

    public int rob(int[] nums) {
        int n = nums.length;


        int[] dp = new int[n];
        Arrays.fill(dp, -1);

        int res = find(n-1, nums, dp);

        return res;

    }
}
```

<hr>

> ### Tabulation
>
> -   Time : O( n )
> -   Space : O( n ) with NO Auxillary Stack Space

```java
class Solution{
    public int rob(int[] nums) {
        int n = nums.length;

        int[] dp = new int[n];
        dp[0] = nums[0];

        for(int i=1; i<n; i++)
        {
            int take = nums[i];
            if(i-2>=0)
            {
                take = nums[i] + dp[i-2];
            }
            int notTake = 0 + dp[i-1];
            dp[i] = Math.max(take, notTake);
        }
        return dp[n-1];

    }
}
```

> ### Space Optimized Solution 
>
> -   Time : O( n )
> -   Space : O( 1 ) with NO Auxillary Stack Space

```java
class Solution{
        public int rob(int[] nums) {
        int n = nums.length;

        int prev2 = 0;
        int prev = nums[0];

        for(int i=1; i<n; i++)
        {
            int take = nums[i];
            if(i-2>=0)
            {
                take = nums[i] + prev2;
            }

            int notTake = 0 + prev;
            
            int curr = Math.max(take, notTake);

            prev2 = prev;
            prev = curr;
        }
        return prev;
    }
}
```
