## [数组跳跃](https://leetcode-cn.com/problems/jump-game/)
题目大意：给定一个数组，每个数组的值代表在当前点向后跳的最大长度，问能否跳到最后一个数。  
分析：这是一个序列存在dp。  
定状态：  
最后一步：如果能跳到第n个数，我们考虑他的最后一步，一定是从第i个位置跳过来的，故此时有num[i] + i >= n  
原问题：是否能跳到n     
子问题：是否能跳到i  
状态dp[i]代表是否跳到i  
求方程：  
dp[i] = dp[j]&&(num[j]+j >= i) 其中j<i  
判边界：  
dp[0] = true
```cpp
//会TLE错误
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        vector<bool> dp(n,false);
        dp[0] = true;
        for(int i = 1;i < n;++i)
        for(int j = 0;j < i;++j)
        if(dp[j]&&(nums[j] + j >= i))
        {
            dp[i] = true;
            break;
        }
        return dp[n-1];
    }
```
我们从另一个角度来dp会发现线性的算法。关键的问题在于状态的定义不同。  
定状态：  
最后一步：从n-1跳到n，记录下最大的值，即max(dp[n-1],n+dp[n])  
原问题：前n个位置能够到达的最大下标  
子问题：前n-1个位置能够到达的最大下标  
dp[i]代表前i个数字能到达的最大下标  
求方程：  
dp[i] = max(dp[i-1],i+nums[i])  
判边界：  
dp[0] = num[0]  
```cpp
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
        return false;
        if(n == 1)
        return true;
        vector<int> dp(n,0);
        dp[0] = nums[0];

        for(int i = 1;i < n;++i)
        if(i > dp[i-1]) //i-1 cant achieve i
        return false;
        else
        {
            dp[i] = max(dp[i-1],i+nums[i]);
            if(dp[i] >= n-1)
            return true;
        }
        return false;
    }
```

