# [dfs](https://leetcode-cn.com/problems/surrounded-regions/submissions/)
对边界区域的O进行dfs，然后将O改为A，之后再遍历整个map，A改为O，O改为X
```cpp
    int dir[4][2] = {0,1,0,-1,-1,0,1,0};
    void dfs(vector<vector<char>>& board,int x,int y)
    {
        board[x][y] = 'A';
        for(int i = 0;i < 4;++i)
        {
            int xx = x + dir[i][0];
            int yy = y + dir[i][1];
            if(xx >= 0 && yy >= 0&&xx < board.size()&&yy < board[0].size()&&board[xx][yy]=='O')
                dfs(board,xx,yy);
        }
    }
    void solve(vector<vector<char>>& board) {
        int n = board.size();
        if(n == 0)
        return ;
        int m = board[0].size();
        for(int i = 0;i < n;++i)
        for(int j = 0;j < m;++j)
        if((i == 0||j == 0||i == n-1||j == m-1)&&board[i][j] =='O')
            dfs(board,i,j);
        
        for(int i = 0;i < n;++i)
        for(int j = 0;j < m;++j)
        if(board[i][j] == 'A')
        board[i][j] = 'O';
        else if(board[i][j] == 'O')
        board[i][j] = 'X';
    }
```
