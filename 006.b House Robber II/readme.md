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
        if(n==1)
        {
            return nums[0];
        }

        int[] arr1 = new int[n-1];
        int[] arr2 = new int[n-1];
        int i1=0;
        int i2=0;
        for(int i=0; i<n; i++)
        {
            if(i!=n-1)
                arr1[i1++] = nums[i];

            if(i!=0)
                arr2[i2++] = nums[i];
        }

        int[] dp1 = new int[arr1.length];
        int[] dp2 = new int[arr2.length];

        Arrays.fill(dp1, -1);
        int first = find(arr1.length-1, arr1, dp1);

        Arrays.fill(dp2, -1);
        int last = find(arr2.length-1, arr2, dp2);

        return Math.max(first, last);
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
        if(n==1)
        {
            return nums[0];
        }

        int[] arr1 = new int[n-1];
        int[] arr2 = new int[n-1];
        int i1=0;
        int i2=0;
        for(int i=0; i<n; i++)
        {
            if(i!=n-1)
                arr1[i1++] = nums[i];

            if(i!=0)
                arr2[i2++] = nums[i];
        }

        int[] dp1 = new int[arr1.length];
        int[] dp2 = new int[arr2.length];

        dp1[0] = arr1[0];
        dp2[0] = arr2[0];

        int len = arr1.length;
        for(int i=1; i<len; i++)
        {
            int take1 = arr1[i];
            int take2 = arr2[i];
            if(i-2>=0)
            {
                take1 = arr1[i] + dp1[i-2];
                take2 = arr2[i] + dp2[i-2];
            }

            int notTake1 = 0 + dp1[i-1];
            int notTake2 = 0 + dp2[i-1];

            dp1[i] = Math.max(take1, notTake1);
            dp2[i] = Math.max(take2, notTake2);
        }
        return Math.max(dp1[len-1], dp2[len-1]);
    }
}
```
<hr>

> ### Space Optimized Solution
>
> -   Time : O( n )
> -   Space : O( 1 ) with NO Auxillary Stack Space

```java
class Solution{
   public int rob(int[] nums) {
        int n = nums.length;
        if(n==1)
        {
            return nums[0];
        }

        int[] arr1 = new int[n-1];
        int[] arr2 = new int[n-1];
        int i1=0;
        int i2=0;
        for(int i=0; i<n; i++)
        {
            if(i!=n-1)
                arr1[i1++] = nums[i];

            if(i!=0)
                arr2[i2++] = nums[i];
        }

        int prev2_dp1 = 0, prev2_dp2 = 0;

        int prev_dp1= arr1[0];
        int prev_dp2 = arr2[0];

        int len = arr1.length;
        for(int i=1; i<len; i++)
        {
            int take1 = arr1[i];
            int take2 = arr2[i];
            if(i-2>=0)
            {
                take1 = arr1[i] + prev2_dp1;
                take2 = arr2[i] + prev2_dp2;
            }

            int notTake1 = 0 + prev_dp1;
            int notTake2 = 0 + prev_dp2;

            prev2_dp1 = prev_dp1;
            prev2_dp2 = prev_dp2;
            prev_dp1 = Math.max(take1, notTake1);
            prev_dp2 = Math.max(take2, notTake2);
        }
        return Math.max(prev_dp1, prev_dp2);
    }
}
```
