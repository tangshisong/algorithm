## [坐标路径](https://leetcode-cn.com/problems/unique-paths/)
题目大意：求从(0,0)点走到(m,n)点的方案数，每次只能向下走或向右走。  
分析：这是一个坐标型的计数问题。  
定状态：  
最后一步：只有从(m-1,n)或(m,n-1)走到(m,n)    
原问题：有多少种方式可以从(0,0)走到(m,n)     
子问题：有多少种方式可以从(0,0)走到(m-1,n)或(m,n-1)   
dp[i][j] = 有多少种方式从从(0,0)走到(i,j)     
求方程：   
dp[i][j] = dp[i-1][j] + dp[i][j-1]  
判边界：  
dp[0][j] = dp[i][0] = 1，只有一种方案。  
```cpp
    int uniquePaths(int m, int n) {
        int dp[100][100];
        memset(dp,0,sizeof(dp));
        for(int i = 0;i < m;++i)
        for(int j = 0;j < n;++j)
        {
            if(i == 0||j == 0)
            dp[i][j] = 1;
            else
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
        return dp[m-1][n-1];
    }
```
