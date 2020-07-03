
# [暴力搜索](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
题目类型：A有n种选择，B有m种选择，求他们所有的选择方案    
手段：暴力搜索   
```cpp
class Solution {
public:
    vector<string> ans;
    void dfs(string temp,string digits,int k,vector<string>& mp)
    {
        if(temp.size() == digits.size())
        {
            ans.push_back(temp);
            return ;
        }
        for(int i = 0;i < mp[digits[k]-'1'].size();++i)
        {
            temp += mp[digits[k]-'1'][i];
            dfs(temp,digits,k+1,mp);
            temp.pop_back();
        }
    }
    vector<string> letterCombinations(string digits) {
        if(digits.size() == 0)
        return ans;
        vector<string> mp(9);
        mp[1] = "abc";
        mp[2] = "def";
        mp[3] = "ghi";
        mp[4] = "jkl";
        mp[5] = "mno";
        mp[6] = "pqrs";
        mp[7] = "tuv";
        mp[8] = "wxyz";
        string temp;
        dfs(temp,digits,0,mp);
        return ans;
    }
};
```
