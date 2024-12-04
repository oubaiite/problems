#include <bits/stdc++.h>
#define fast ios::sync_with_stdio(0);cin.tie(0);cout.tie(0);
#define ll long long
using namespace std;
char board[8][8];
bool queens[8][8];
int ok;
bool checkRow(int row)
{
    int cnt = 0;
    for (int i = 0; i < 8; i++)
    {
        if (queens[row][i])
            cnt++;
    }
    if (cnt > 1)
        return 0;
    return 1;
}
bool checkCol(int col)
{
    int cnt = 0;
    for (int i = 0; i < 8; i++)
    {
        if (queens[i][col])
            cnt++;
    }
    if (cnt > 1)
        return 0;
    return 1;
}
bool checkDigonals(int row, int col)
{
    int cnt = 0;
    int i = row, j = col;
    while (i>=0&&j>=0)
    {
        if (queens[i][j])
            cnt++;
        i--, j--;
    }
    i = row + 1, j = col + 1;
    while (i <8 && j<8)
    {
        if (queens[i][j])
            cnt++;
        i++, j++;
    }
    if (cnt > 1)
        return 0;
    cnt = 0;
    i = row, j = col;
    while (i>=0&&j<8)
    {
        if (queens[i][j])
            cnt++;
        i--, j++;
    }
    i = row + 1, j = col - 1;
    while (i < 8 && j >= 0)
    {
        if (queens[i][j])
            cnt++;
        i++, j--;
    }
    if (cnt > 1)
        return 0;
    return 1;
}
void bactTraking(int i, int j, int q)
{
    if (q == 0)
    {
        ok++;
        return;
    }
    if (i == 8)
        return;
    int ii = i, jj = j;
    if (j != 7)
        jj++;
    else
    {
        ii++;
        jj = 0;
    }
    if (board[i][j] == '*')
    {
        bactTraking(ii, jj, q);
    }
    else
    {
        queens[i][j] = 1;
        if (checkCol(j) && checkRow(i) && checkDigonals(i,j))
            bactTraking(ii, jj, q - 1);
        queens[i][j] = 0;
        bactTraking(ii,jj, q);
    }
}
int divisior(long long x)
{
    int ans=0;
    for(int i=1;i*i<=x;i++)
    {
        if(x%i==0)
        {
           ans++;
            if(i*i!=x)
            ans++;
        }
    }
    return ans;
}
int main()
{
 for (int i = 0; i < 8; i++)
{
    for (int j = 0;j < 8; j++)
    {
        cin >> board[i][j];
    }
}
bactTraking(0, 0, 8);
cout << ok;
}
