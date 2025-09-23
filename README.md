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
