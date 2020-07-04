# []()
```cpp
//string substr(int pos = 0,int n = npos) const;//返回pos开始的n个字符组成的字符串
//string &erase(int pos = 0, int n = npos);//删除pos开始的n个字符，返回修改后的字符串
class Solution {
public:
    vector<string> ans;
    bool valid(string x)
    {
        if(x.empty() || (x[0] == '0' && x.size() > 1))
        return false;
        int f = stoi(x);
        if(f >= 0 && f <= 255)
        return true;
        return false;
    }
    void dfs(string s,string temp,int num)
    {
        //四段数据都找到为终止条件且不剩余字符
        if(num == 4 && s.empty())
        {

            ans.push_back(temp);
            return ;
        }

        if(num > 0)
        temp += ".";
        for(int i = 1;i <= 3 && i <= s.length();++i)//扩展方式（下一次选的字符是1.3的个数）
        if(valid(s.substr(0,i)))
        {
            temp += s.substr(0,i);
            dfs(s.substr(i,s.length()-i),temp,num+1);
            temp.erase(temp.length()-i,i);
        }
    }
    vector<string> restoreIpAddresses(string s) {
        if(s.size() < 4 || s.size() > 12)
        return ans;
        string temp;
        dfs(s,temp,0);
        return ans;
    }
};
```
