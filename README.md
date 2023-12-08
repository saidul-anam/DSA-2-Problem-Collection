# DSA-2-Problem-Collection

# Contents

## [Minimum Spanning Tree](#Problems)
## [Single Source Shortest Path](#Problems)

# Minimum Spanning Tree

# Problems

>1) A Civil Engineer is given a task to connect n houses with the main electric power station directly or indirectly. The Govt has given him permission to connect exactly n wires to connect all of them. Each of the wires connects either two houses, or a house and the power station. The costs for connecting each of the wires are given.
Since the Civil Engineer is clever enough and tries to make some profit, he made a plan. His plan is to find the best possible connection scheme and the worst possible connection scheme. Then he will report the average of the costs.
Now you are given the task to check whether the Civil Engineer is evil or not. That's why you want to calculate the average before he reports to the Govt.

Original Problem Link : https://lightoj.com/problem/civil-and-evil-engineer<br>
1).Solution 
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
class unionfined{
int *parent;
int *Rank;
public:
unionfined(int i){
    parent=new int[i];
    Rank=new int[i];
    for(int j=0;j<i+1;j++){
        parent[j]=j;
        Rank[j]=0;
    }
    }
    int Findparent(int i){
if(parent[i]==i){
    return i;
}
else return parent[i]=Findparent(parent[i]);
}
void unionset(int u,int v){
u=Findparent(u);
v=Findparent(v);
if(Rank[u]<Rank[v]){
    parent[u]=v;
}
else if(Rank[v]<Rank[u]) {
    parent[v]=u;
}
else{
    parent[v]=u;
    Rank[u]++;
}
}
};
class mst{
int minweight;
int k;
public:
    mst(int i){
        k=i;
            }
int getmst(vector<vector<int>>arr1){
    vector<vector<int>>arr=arr1;
    sort(arr.begin(),arr.end());
    minweight=0;
    unionfined x(k);
for(int i=0;i<arr.size();i++){
        int start=x.Findparent(arr[i][1]);
        int finish=x.Findparent(arr[i][2]);
     if(start!=finish){
            minweight+=arr[i][0];
        x.unionset(start,finish);
     }
}
for(int i=0;i<=k;i++){
    if(x.Findparent(i)!=x.Findparent(1)){
        return INT_MAX;
    }
}
return minweight;
}
};
bool cmp1(vector<int>&a,vector<int>&b){
return a[0]>b[0];}
class wst{
int highweight;
int k;
public:
    wst(int i){
        k=i;
            }
int getwst(vector<vector<int>>arr1){
    vector<vector<int>>arr2=arr1;
    sort(arr2.begin(),arr2.end(),cmp1);
    highweight=0;
    unionfined x(k);
for(int i=0;i<arr2.size();i++){
        int start=x.Findparent(arr2[i][1]);
        int finish=x.Findparent(arr2[i][2]);
     if(start!=finish){
            highweight+=arr2[i][0];
        x.unionset(start,finish);
     }
}
for(int i=0;i<=k;i++){
    if(x.Findparent(i)!=x.Findparent(1)){
        return -1;
    }
}
return highweight;
}
};

void solve(){
 int x;
 cin>>x;
 vector<vector<int>>arr;
 while(true){
    int a,b,c;
    cin>>a>>b>>c;
    if(a==0&&b==0&&c==0){
        break;
    }
    arr.push_back({c,a,b});
    }
    mst ab(x);
 int minweight=ab.getmst(arr);
 wst ac(x);
 int highweight=ac.getwst(arr);
 int ans=(minweight+highweight);
 if(ans%2==0){
 cout<<ans/2<<endl;}
 else{
    cout<<ans<<"/2"<<endl;
 }
}


int main(){
 int n;
 cin>>n;
 int i=1;
 while(n--){
        cout<<"Case "<<i<<": ";
        i++;
    solve();
 }
}
```


# Single Source Shortest Path

# Problems
>a. Write an SQL query to retrieve all country names.<br>
