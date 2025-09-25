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
