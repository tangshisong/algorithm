如果想不出更好的算法，就首选dp和dfs，如果求种类和可能性问题就用dp，求具体方案就dfs（这个代码在dfs部分的《部分和》中有具体描述）.
# dp求ksum的方案数
* 定状态  
最后一步：从n-k+1个数字中选第k个数字满足其总和为sum   
原问题：从n个数字中选取k个数字满足其总和为sum     
子问题：从n-1个数字中选取k-1个数字满足其总和为sum-num[k]   
所以这里有三个状态我们需要记录，故定义状态dp[i][j][s]代表从前i个数字中选取j个数使得其和为s   
* 求方程  
对于每一个位置，只有选还是不选的分别：dp[i][j][s] = dp[i-1][j-1][s-num[i]] + dp[i-1][j][s]   
如果为可能性问题：dp[i][j][s] =  dp[i-1][j-1][s-num[i]] || dp[i-1][j][s]   
* 判边界     
dp[i][0][0] 代表空，赋值为1    
# [有序2sum](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)
1. 如果数组已经排序，采用双指针法，sum小就++i，sum大就--j，时间复杂度为O（N）      
```cpp
    vector<int> twoSum(vector<int>& numbers, int target) {
        int i = 0;
        int j= numbers.size()-1;
        vector<int> ans;
        while(i < j)
        {
            if(numbers[i] + numbers[j] == target)
            {
                ans.push_back(i+1);
                ans.push_back(j+1);
                return ans;
            }
            else if(numbers[i] + numbers[j] > target)
            --j;
            else 
            ++i;
        }

        return ans;
    }
```
# [无序2sum](https://leetcode-cn.com/problems/two-sum/)
2. 如果没有排序，就采用hashmap，不断存放差值，时空复杂度都为O（N）   
```cpp
    vector<int> twoSum(vector<int>& nums, int target) {
        //采用map一次遍历
        map<int,int> mp;
        vector<int> ans;
        int n = nums.size();
        map<int,int>::iterator it;

        for(int i = 0;i < n;++i)
        {
            int t = target - nums[i];//差值
            it = mp.find(nums[i]);//看前面是否存在target-nums[i]的差值
            if(it == mp.end())//不存在就记录下来差值
            mp[t] = i;
            else //如果存在就找到答案
            {
                ans.push_back(mp[nums[i]]);
                ans.push_back(i);
            }
        }
        return ans;
    }
```
# [3sum]()

# [4sum]()

# [ksum]()

# [3-closed sum]()
