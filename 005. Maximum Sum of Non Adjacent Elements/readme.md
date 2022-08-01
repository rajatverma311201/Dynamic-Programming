> ### Brute force Recursive Soln
>
> -   Time : O( 2<sup>n</sup> )
> -   Space : O( 1 ) + Auxillary Stack Space

```java
import java.util.*;
public class Solution {
    public static int giveMax(int ind, ArrayList<Integer> nums)
    {
        if(ind==0)
        {
            return nums.get(ind);
        }
        if(ind<0)
        {
            return 0;
        }

        //  pick the current element
        int pick = nums.get(ind) + giveMax(ind-2, nums);

        //  don't pick the current element
        int notPick = giveMax(ind-1, nums);

        return Math.max(pick, notPick);
    }

	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
		// Write your code here.
        return giveMax(nums.size()-1, nums);
	}
}
```

<hr>

> ### Memoized Recursion Approach
>
> -   Time : O( n )
> -   Space: O( n ) + Auxillary Stack Space

```java
import java.util.*;
public class Solution {
    public static int giveMax(int ind, ArrayList<Integer> nums, int[] dp)
    {
        if(ind==0)
        {
            return nums.get(ind);
        }
        if(ind<0)
        {
            return 0;
        }
        if(dp[ind]!=-1)
        {
            return dp[ind];
        }
        //  pick the current element
        int pick = nums.get(ind) + giveMax(ind-2, nums, dp);

        //  don't pick the current element
        int notPick = giveMax(ind-1, nums, dp);

        return dp[ind] = Math.max(pick, notPick);
    }

	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
        int[] dp = new int[nums.size()];
        Arrays.fill(dp, -1);
        return giveMax(nums.size()-1, nums, dp);
	}
}
```

<hr>

> ### Tabulation
>
> -   Time : O( n )
> -   Space : O( n ) with NO Auxillary Stack Space

```java
public class Solution{
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
        int[] dp = new int[nums.size()];

        dp[0] = nums.get(0);
        int neg = 0;

        for(int i=1; i<nums.size(); i++)
        {
            int pick;
            if(i-2>=0)
            {
                pick = nums.get(i) + dp[i-2];
            }
            else
            {
                pick = nums.get(i) + neg;
            }

            int notPick = 0 + dp[i-1];

            dp[i] = Math.max(pick, notPick);
        }

        return dp[nums.size()-1];
	}
}
```

> ### Space Optimization
>
> -   Time : O( n )
> -   Space : O( 1 )

```java
public class Solution{
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
        int[] dp = new int[nums.size()];

        int prev2 = 0;
        int prev = nums.get(0);
        int curr = 0;

        for(int i=1; i<nums.size(); i++)
        {
            int pick;
            if(i-2>=0)
            {
                pick = nums.get(i) + prev2;
            }
            else
            {
                pick = nums.get(i) + 0;
            }
            int notPick = 0 + prev;

            curr = Math.max(pick, notPick);

            prev2 = prev;
            prev = curr;
        }
        return prev;
	}
}
```
