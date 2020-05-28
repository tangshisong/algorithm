# [有序2sum](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/
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
