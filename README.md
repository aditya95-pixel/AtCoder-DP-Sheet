### A - Frog 1  

Problem Statement
There are 
N stones, numbered 
1,2,…,N. For each 
i (
1≤i≤N), the height of Stone 
i is 
h 
i
​
 .

There is a frog who is initially on Stone 
1. He will repeat the following action some number of times to reach Stone 
N:

If the frog is currently on Stone 
i, jump to Stone 
i+1 or Stone 
i+2. Here, a cost of 
∣h 
i
​
 −h 
 j∣ is incurred, where 
j is the stone to land on.
Find the minimum possible total cost incurred before the frog reaches Stone 
N.
​
```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
int32_t main(){
    int n;
    cin>>n;
    vector<int>heights(n);
    for(auto &ele:heights)
    cin>>ele;
    vector<int>dp(n,INT_MAX);
    dp[0]=0;
    dp[1]=abs(heights[1]-heights[0]);
    for(int i=2;i<n;i++){
        dp[i]=min(dp[i-1]+abs(heights[i]-heights[i-1]),
                dp[i-2]+abs(heights[i]-heights[i-2]));
    }
    cout<<dp[n-1]<<endl;
}
```

### B Frog 2

There are 
N stones, numbered 
1,2,…,N. For each 
i (
1≤i≤N), the height of Stone 
i is 
h 
i
​
 .

There is a frog who is initially on Stone 
1. He will repeat the following action some number of times to reach Stone 
N:

If the frog is currently on Stone 
i, jump to one of the following: Stone 
i+1,i+2,…,i+K. Here, a cost of 
∣h 
i
​
 −h 
j
​
 ∣ is incurred, where 
j is the stone to land on.
Find the minimum possible total cost incurred before the frog reaches Stone 
N.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
int32_t main(){
    int n,k;
    cin>>n>>k;
    vector<int>heights(n);
    for(auto &ele:heights)
    cin>>ele;
    vector<int>dp(n,INT_MAX);
    dp[0]=0;
    dp[1]=abs(heights[1]-heights[0]);
    for(int i=2;i<n;i++){
        for(int j=1;j<=k;j++)
        {
            if(i-j>=0)
            dp[i]=min(dp[i],dp[i-j]+abs(heights[i]-heights[i-j]));
        } 
    }
    cout<<dp[n-1]<<endl;
}
```

### C Vacation

Problem Statement
Taro's summer vacation starts tomorrow, and he has decided to make plans for it now.

The vacation consists of 
N days. For each 
i (
1≤i≤N), Taro will choose one of the following activities and do it on the 
i-th day:

A: Swim in the sea. Gain 
a 
i
​
  points of happiness.
B: Catch bugs in the mountains. Gain 
b 
i
​
  points of happiness.
C: Do homework at home. Gain 
c 
i
​
  points of happiness.
As Taro gets bored easily, he cannot do the same activities for two or more consecutive days.

Find the maximum possible total points of happiness that Taro gains.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
int32_t main(){
    int n;
    cin>>n;
    vector<int>a(n),b(n),c(n);
    for(int i=0;i<n;i++){
        cin>>a[i]>>b[i]>>c[i];
    }
    vector<vector<int>>dp(n+1,vector<int>(3,0));
    dp[0][0]=0;
    dp[0][1]=0;
    dp[0][2]=0;
    for(int i=1;i<=n;i++){
        dp[i][0]=max(dp[i-1][1]+a[i-1],dp[i-1][2]+a[i-1]);
        dp[i][1]=max(dp[i-1][0]+b[i-1],dp[i-1][2]+b[i-1]);
        dp[i][2]=max(dp[i-1][0]+c[i-1],dp[i-1][1]+c[i-1]);
    }
    cout<<max({dp[n][0],dp[n][1],dp[n][2]});
}
```

### D Knapsack 1

Problem Statement
There are 
N items, numbered 
1,2,…,N. For each 
i (
1≤i≤N), Item 
i has a weight of 
w 
i
​
  and a value of 
v 
i
​
 .

Taro has decided to choose some of the 
N items and carry them home in a knapsack. The capacity of the knapsack is 
W, which means that the sum of the weights of items taken must be at most 
W.

Find the maximum possible sum of the values of items that Taro takes home.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
int32_t main(){
    int n,w;
    cin>>n>>w;
    vector<int>weights(n),values(n);
    for(int i=0;i<n;i++){
        cin>>weights[i]>>values[i];
    }
    vector<vector<int>>dp(n+1,vector<int>(w+1,0));
    for(int i=1;i<=n;i++){
        for(int j=0;j<=w;j++){
            dp[i][j]=dp[i-1][j];
            if(j-weights[i-1]>=0)
            dp[i][j]=max(dp[i][j],dp[i-1][j-weights[i-1]]+values[i-1]);
        }
    }
    cout<<dp[n][w];
}
```

### E Knapsack 2

Problem Statement
There are 
N items, numbered 
1,2,…,N. For each 
i (
1≤i≤N), Item 
i has a weight of 
w 
i
​
  and a value of 
v 
i
​
 .

Taro has decided to choose some of the 
N items and carry them home in a knapsack. The capacity of the knapsack is 
W, which means that the sum of the weights of items taken must be at most 
W.

Find the maximum possible sum of the values of items that Taro takes home.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n,w;
    cin>>n>>w;
    vector<int>weights(n),values(n);
    int V=0;
    for(int i=0;i<n;i++){
        cin>>weights[i]>>values[i];
        V+=values[i];
    }
    vector<int>dp(V+1,INF);
    dp[0]=0;
    for(int i=0;i<n;i++)
    {
        for(int v=V;v>=values[i];v--)
        dp[v]=min(dp[v],dp[v-values[i]]+weights[i]);
    }
    int res=0;
    for(int v=0;v<=V;v++){
        if(dp[v]<=w)
        res=v;
    }
    cout<<res<<endl;
}
```

### F LCS

Problem Statement
You are given strings 
s and 
t. Find one longest string that is a subsequence of both 
s and 
t.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    string s,t;
    cin>>s>>t;
    vector<vector<int>>dp(s.size()+1,vector<int>(t.size()+1,0));
    for(int i=1;i<=s.size();i++){
        for(int j=1;j<=t.size();j++){
            if(s[i-1]==t[j-1])
            dp[i][j]=dp[i-1][j-1]+1;
            else
            dp[i][j]=max({dp[i-1][j],dp[i][j-1]});
        }
    }
    string res;
    int i=s.size(),j=t.size();
    while(i>0 && j>0){
        if(s[i-1]==t[j-1])
        {
            res+=s[i-1];
            i--;
            j--;
        }
        else if(dp[i-1][j]>dp[i][j-1])
            i--;
        else
            j--;
    }
    reverse(res.begin(),res.end());
    cout<<res<<endl;
}
```

### G Longest Path (DP on DAG concept)

There is a directed graph 
G with 
N vertices and 
M edges. The vertices are numbered 
1,2,…,N, and for each 
i (
1≤i≤M), the 
i-th directed edge goes from Vertex 
x 
i
​
  to 
y 
i
​
 . 
G does not contain directed cycles.

Find the length of the longest directed path in 
G. Here, the length of a directed path is the number of edges in it.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n,m;
    cin>>n>>m;
    vector<vector<int>>adj(n+1);
    vector<int>indeg(n+1,0);
    for(int i=0;i<m;i++){
        int x,y;
        cin>>x>>y;
        adj[x].push_back(y);
        indeg[y]++;
    }
    queue<int>q;
    for(int i=1;i<=n;i++)
    {
        if(indeg[i]==0)
        q.push(i);
    }
    vector<int>dp(n+1,0);
    while(!q.empty()){
        int u=q.front();
        q.pop();
        for(auto v:adj[u]){
            indeg[v]--;
            dp[v]=max(dp[v],dp[u]+1);
            if(indeg[v]==0)
                q.push(v);
        }
    }
    cout<<*max_element(dp.begin(),dp.end());
}
```

### H Grid 1

There is a grid with 
H horizontal rows and 
W vertical columns. Let 
(i,j) denote the square at the 
i-th row from the top and the 
j-th column from the left.

For each 
i and 
j (
1≤i≤H, 
1≤j≤W), Square 
(i,j) is described by a character 
a 
i,j
​
 . If 
a 
i,j
​
  is ., Square 
(i,j) is an empty square; if 
a 
i,j
​
  is #, Square 
(i,j) is a wall square. It is guaranteed that Squares 
(1,1) and 
(H,W) are empty squares.

Taro will start from Square 
(1,1) and reach 
(H,W) by repeatedly moving right or down to an adjacent empty square.

Find the number of Taro's paths from Square 
(1,1) to 
(H,W). As the answer can be extremely large, find the count modulo 
10 
9
 +7.

 ```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int h,w;
    cin>>h>>w;
    vector<string>grid;
    for(int i=0;i<h;i++){
        string str;
        cin>>str;
        grid.push_back(str);
    }
    vector<vector<int>>dp(h,vector<int>(w,0));
    if(grid[0][0]=='#')
    {cout<<0<<endl;return 0;}
    dp[0][0]=1;
    for(int i=0;i<h;i++){
        for(int j=0;j<w;j++){
            if(dp[i][j]>0 && i+1<h && grid[i+1][j]=='.')
            dp[i+1][j]=(dp[i+1][j]+dp[i][j])%MOD;
            if(dp[i][j]>0 && j+1<w && grid[i][j+1]=='.')
            dp[i][j+1]=(dp[i][j+1]+dp[i][j])%MOD;
        }
    }
    cout<<dp[h-1][w-1]<<endl;
}
```

### I Coins (DP on Probability)

Problem Statement
Let 
N be a positive odd number.

There are 
N coins, numbered 
1,2,…,N. For each 
i (
1≤i≤N), when Coin 
i is tossed, it comes up heads with probability 
p 
i
​
  and tails with probability 
1−p 
i
​
 .

Taro has tossed all the 
N coins. Find the probability of having more heads than tails.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n;
    cin>>n;
    vector<double>prob(n);
    for(auto &p:prob)
    cin>>p;
    vector<double>dp(n+1,0);
    dp[0]=1;
    for(int i=0;i<n;i++){
        for(int j=i+1;j>=0;j--)
            dp[j]=(j>0?dp[j-1]:0)*prob[i]+dp[j]*(1-prob[i]);
    }
    double sum=0;
    for(int i=(n+1)/2;i<=n;i++)
    sum+=dp[i];
    cout<<setprecision(10)<<sum<<endl;
}
```

### J Sushi

There are 
N dishes, numbered 
1,2,…,N. Initially, for each 
i (
1≤i≤N), Dish 
i has 
a 
i
​
  (
1≤a 
i
​
 ≤3) pieces of sushi on it.

Taro will perform the following operation repeatedly until all the pieces of sushi are eaten:

Roll a die that shows the numbers 
1,2,…,N with equal probabilities, and let 
i be the outcome. If there are some pieces of sushi on Dish 
i, eat one of them; if there is none, do nothing.
Find the expected number of times the operation is performed before all the pieces of sushi are eaten.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n;
    cin>>n;
    vector<int>a(n);
    int c1=0,c2=0,c3=0;
    for(auto &ele:a)
    {
        cin>>ele;
        if(ele==1)
        c1++;
        else if(ele==2)
        c2++;
        else
        c3++;
    }
    vector<vector<vector<double>>>dp(n+1,vector<vector<double>>(n+1,vector<double>(n+1,0)));
    dp[0][0][0]=0;
    for(int s=1;s<=n;s++){
        for(int i=s;i>=0;i--){
            for(int j=s-i;j>=0;j--){
                int k=s-i-j;
                if(k<0 || k>n)
                continue;
                double term=n;
                if(i>0) term+=i*dp[i-1][j][k];
                if(j>0) term+=j*dp[i+1][j-1][k];
                if(k>0) term+=k*dp[i][j+1][k-1];
                dp[i][j][k]=term/s;
            }
        }
    }
    cout<<setprecision(10)<<dp[c1][c2][c3]<<endl;
}
```

### K Stones

There is a set 
A={a 
1
​
 ,a 
2
​
 ,…,a 
N
​
 } consisting of 
N positive integers. Taro and Jiro will play the following game against each other.

Initially, we have a pile consisting of 
K stones. The two players perform the following operation alternately, starting from Taro:

Choose an element 
x in 
A, and remove exactly 
x stones from the pile.
A player loses when he becomes unable to play. Assuming that both players play optimally, determine the winner.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n,k;
    cin>>n>>k;
    vector<int>a(n);
    for(auto &ele:a)
    cin>>ele;
    vector<int>dp(k+1,0);
    dp[0]=0;
    for(int i=1;i<=k;i++){
        for(auto x:a)
        {
            if(i>=x && !dp[i-x])
            dp[i]=1;
        }
    }
    if(dp[k])
    cout<<"First";
    else
    cout<<"Second";
}
```

### L Deque

Taro and Jiro will play the following game against each other.

Initially, they are given a sequence 
a=(a 
1
​
 ,a 
2
​
 ,…,a 
N
​
 ). Until 
a becomes empty, the two players perform the following operation alternately, starting from Taro:

Remove the element at the beginning or the end of 
a. The player earns 
x points, where 
x is the removed element.
Let 
X and 
Y be Taro's and Jiro's total score at the end of the game, respectively. Taro tries to maximize 
X−Y, while Jiro tries to minimize 
X−Y.

Assuming that the two players play optimally, find the resulting value of 
X−Y.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n;
    cin>>n;
    vector<int>a(n);
    for(auto &ele:a)
    cin>>ele;
    vector<vector<int>>dp(n,vector<int>(n,0));
    for(int len=1;len<=n;len++){
        for(int l=0;l+len-1<n;l++){
            int r=l+len-1;
            if(len==1)
            dp[l][r]=a[l];
            else
            dp[l][r]=max(a[l]-dp[l+1][r],a[r]-dp[l][r-1]);
        }
    }
    cout<<dp[0][n-1]<<endl;
}
```

### M Candies

There are 
N children, numbered 
1,2,…,N.

They have decided to share 
K candies among themselves. Here, for each 
i (
1≤i≤N), Child 
i must receive between 
0 and 
a 
i
​
  candies (inclusive). Also, no candies should be left over.

Find the number of ways for them to share candies, modulo 
10 
9
 +7. Here, two ways are said to be different when there exists a child who receives a different number of candies.

 ```cpp
 #include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n,k;
    cin>>n>>k;
    vector<int>a(n);
    for(auto &ele:a)
    cin>>ele;
    vector<vector<int>>dp(n+1,vector<int>(k+1,0));
    dp[0][0]=1;
    for(int i=1;i<=n;i++){
        vector<int>pref(k+2,0);
        for(int j=0;j<=k;j++)
        pref[j+1]=(pref[j]+dp[i-1][j])%MOD;
        for(int j=0;j<=k;j++){
            int left=max(0LL,j-a[i-1]);
            dp[i][j]=(pref[j+1]-pref[left]+MOD)%MOD;
        }
    }
    cout<<dp[n][k]<<endl;
}
```

### N Slimes

There are 
N slimes lining up in a row. Initially, the 
i-th slime from the left has a size of 
a 
i
​
 .

Taro is trying to combine all the slimes into a larger slime. He will perform the following operation repeatedly until there is only one slime:

Choose two adjacent slimes, and combine them into a new slime. The new slime has a size of 
x+y, where 
x and 
y are the sizes of the slimes before combining them. Here, a cost of 
x+y is incurred. The positional relationship of the slimes does not change while combining slimes.
Find the minimum possible total cost incurred.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n;
    cin>>n;
    vector<int>a(n),pref(n+1,0);
    for(int i=0;i<n;i++){
        cin>>a[i];
        pref[i+1]=pref[i]+a[i];
    } 
    vector<vector<int>>dp(n,vector<int>(n,0));
    for(int len=2;len<=n;len++){
        for(int l=0;l+len-1<n;l++){
            int r=l+len-1;
            dp[l][r]=INT64_MAX;
            for(int k=l;k<r;k++)
            dp[l][r]=min(dp[l][r],dp[l][k]+dp[k+1][r]+pref[r+1]-pref[l]);
        }
    }
    cout<<dp[0][n-1];
}
```

### O Matching (BitMask DP)

There are 
N men and 
N women, both numbered 
1,2,…,N.

For each 
i,j (
1≤i,j≤N), the compatibility of Man 
i and Woman 
j is given as an integer 
a 
i,j
​
 . If 
a 
i,j
​
 =1, Man 
i and Woman 
j are compatible; if 
a 
i,j
​
 =0, they are not.

Taro is trying to make 
N pairs, each consisting of a man and a woman who are compatible. Here, each man and each woman must belong to exactly one pair.

Find the number of ways in which Taro can make 
N pairs, modulo 
10 
9
 +7.

 ```cpp
 #include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
int32_t main(){
    int n;
    cin>>n;
    vector<vector<int>>a(n,vector<int>(n,0));
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            cin>>a[i][j];
        }
    }
    int m=1<<n;
    vector<int>dp(m,0);
    dp[0]=1;
    for(int mask=0;mask<m;mask++){
        int man=__builtin_popcount(mask);
        if(man>=n)
        continue;
        for(int woman=0;woman<n;woman++){
            if((mask & (1<<woman))==0 && a[man][woman]==1)
            {
                int nmask=mask|(1<<woman);
                dp[nmask]=(dp[nmask]+dp[mask])%MOD;
            }
        }
    }
    cout<<dp[m-1]<<endl;
}
```

### P Independent Set

There is a tree with 
N vertices, numbered 
1,2,…,N. For each 
i (
1≤i≤N−1), the 
i-th edge connects Vertex 
x 
i
​
  and 
y 
i
​
 .

Taro has decided to paint each vertex in white or black. Here, it is not allowed to paint two adjacent vertices both in black.

Find the number of ways in which the vertices can be painted, modulo 
10 
9
 +7.

 ```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define MOD 1000000007
const int INF=1e15;
void dfs(int u,int p,vector<vector<int>>&adj,
vector<vector<int>>&dp){
    dp[u][0]=1;
    dp[u][1]=1;
    for(auto v:adj[u]){
        if(v!=p){
            dfs(v,u,adj,dp);
            dp[u][0]=(dp[u][0]*((dp[v][0]+dp[v][1])%MOD))%MOD;
            dp[u][1]=(dp[u][1]*dp[v][0])%MOD;
        }
    }
}
int32_t main(){
    int n;
    cin>>n;
    vector<vector<int>>adj(n+1);
    for(int i=0;i<n-1;i++){
        int x,y;
        cin>>x>>y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    vector<vector<int>>dp(n+1,vector<int>(2,0));
    dfs(1,0,adj,dp);
    int res=(dp[1][0]+dp[1][1])%MOD;
    cout<<res<<endl;
}
```
