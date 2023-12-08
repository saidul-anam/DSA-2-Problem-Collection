# DSA-2-Problem-Collection

# Contents

## [Minimum Spanning Tree](#Problem1,Problem2,Problem3,Problem4)
## [Single Source Shortest Path](#Problems)

# Minimum Spanning Tree
<details>
<summary>Problem</summary>
    
# Problem1

>1) A Civil Engineer is given a task to connect n houses with the main electric power station directly or indirectly. The Govt has given him permission to connect exactly n wires to connect all of them. Each of the wires connects either two houses, or a house and the power station. The costs for connecting each of the wires are given.
Since the Civil Engineer is clever enough and tries to make some profit, he made a plan. His plan is to find the best possible connection scheme and the worst possible connection scheme. Then he will report the average of the costs.
Now you are given the task to check whether the Civil Engineer is evil or not. That's why you want to calculate the average before he reports to the Govt.

Original Problem Link : https://lightoj.com/problem/civil-and-evil-engineer<br>
<details>
<summary>Solution</summary>
    
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
</details>

# Problem2
>2)A local charity is trying to gather donations of Ethernet cable. You realize that you probably have a lot of extra cable in your house, and make the decision that you will donate as much cable as you can spare.
You will be given the lengths (in meters) of cables between each pair of rooms in your house. You wish to keep only enough cable so that every pair of rooms in your house is connected by some chain of cables, of any length. The lengths are given in n lines, each having n integers, where n is the number of rooms in your house. The jthinteger of ith line gives the length of the cable between rooms i and j in your house.
If both the jth integer of ithline and the ith integer of jth line are greater than 0, this means that you have two cables connecting rooms iand j, and you can certainly donate at least one of them. If the ithinteger of ith line is greater than 0, this indicates unused cable in room i, which you can donate without affecting your home network in any way. 0 means no cable.
You are not to rearrange any cables in your house; you are only to remove unnecessary ones. Return the maximum total length of cables (in meters) that you can donate. If any pair of rooms is not initially connected by some path, return -1.

Original Problem Link :https://lightoj.com/problem/donation

 <details>
<summary>Solution</summary>
     
```cpp
#include<bits/stdc++.h>
using namespace std;
class unionfined{
int *parent;
int *Rank;
public:
unionfined(int i){
    parent=new int[i];
    Rank=new int[i];
    for(int j=0;j<i;j++){
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
for(int i=0;i<k;i++){
    if(x.Findparent(i)!=x.Findparent(1)){
        return -1;
    }
}
return minweight;
}
};
void solve(){
 int x;
 cin>>x;
 int ans=0;
 vector<vector<int>>arr;
 for(int i=0;i<x;i++){
     for(int j=0;j<x;j++){
    int c;
    cin>>c;
    ans+=c;
    if(c!=0) arr.push_back({c,i,j});
    }
    }
    mst ab(x);
 int minweight=ab.getmst(arr);


   if(minweight!=-1) cout<<ans-minweight<<endl;
   else cout<<minweight<<endl;

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
</details>

# Problem3
>3)The government of a certain developing nation wants to improve transportation in one of its most inaccessible areas, in an attempt to attract investment. The region consists of several important locations that must have access to an airport.
Of course, one option is to build an airport in each of these places, but it may turn out to be cheaper to build fewer airports and have roads link them to all of the other locations. Since these are long distance roads connecting major locations in the country (e.g. cities, large villages, industrial areas), all roads are two-way. Also, there may be more than one direct road possible between two areas. This is because there may be several ways to link two areas (e.g. one road tunnels through a mountain while the other goes around it etc.) with possibly differing costs.
A location is considered to have access to an airport either if it contains an airport or if it is possible to travel by road to another location from there that has an airport.
You are given the cost of building an airport and a list of possible roads between pairs of locations and their corresponding costs. The government now needs your help to decide on the cheapest way of ensuring that every location has access to an airport. The aim is to make airport access as easy as possible, so if there are several ways of getting the minimal cost, choose the one that has the most airports.

Original source:https://lightoj.com/problem/air-ports

<details>
<summary>Solution</summary>
    
```cpp
#include<bits/stdc++.h>
using namespace std;
class unionfined{
int *parent;
int *Rank;
public:
unionfined(int i){
    parent=new int[i];
    Rank=new int[i];
    for(int j=1;j<=i;j++){
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
void getmst(vector<vector<int>>arr1,int y){
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
     }}
   set<int>component;
for(int i=1;i<=k;i++){
component.insert(x.Findparent(i));
}
cout<<minweight+(component.size()*y)<<" "<<component.size()<<endl;
}
};
void solve(){
 int n,x,y;
 cin>>n>>x>>y;
 vector<vector<int>>arr;
 for(int i=0;i<x;i++){
        int a,b,c;
 cin>>a>>b>>c;
 if(c<y) arr.push_back({c,a,b});
    }
    mst ab(n);
 ab.getmst(arr,y);
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
</details>
            
# Problem4
>4)Given a set of houses, each with the option of having an independent gas supply incurring a
cost 'gas_supply[i]' or connecting to other houses through bidirectional pipelines with associated
costs 'pipelines[i] = [house1, house2, cost]'. The objective is to minimize the total cost of
ensuring gas supply to all houses, considering both independent gas supplies and pipeline
connections. In other words, we want to find the most cost-effective way to provide gas to all
houses, allowing for a mix of individual gas supplies and interconnected pipelines.

Input <br>
The first input line contains two integers, n and m, representing the number of houses and the
number of bidirectional pipelines. Following that, there is an array gas_supply of length n, where
gas_supply[i] represents the cost of providing independent gas supply to the ith house. The
values should be space-separated. The next m lines each contain three space-separated
integers: house1, house2, and cost (1 <= house1, house2 <= n, 1 <= cost <= 1000). These
values represent the cost of connecting house1 and house2 with a bidirectional pipeline of cost
'cost'

Output<br>
Your program should print a single integer to the standard output, representing the minimum
total cost of ensuring gas supply to all house

Example<br>
| Input | Output|
|--|--|
|4 2   |8|
1 4 4 4
1 4 2
1 2 1  

<details>
<summary>Solution</summary>
    
```cpp
#include<bits/stdc++.h>
using namespace std;
vector<int>arr5(1000,-1);
class unionfined{
int *parent;
int *Rank;
public:
unionfined(int i){
    parent=new int[i+1];
    Rank=new int[i+1];
    for(int j=1;j<=i;j++){
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
void getmst(vector<vector<int>>arr1){
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
     }}
   set<int>component;
for(int i=1;i<=k;i++){
component.insert(x.Findparent(i));}
for(int i=0;i<component.size();i++){
        int host=INT_MAX;
for(int j=1;j<=k;j++){
    if(x.Findparent(j)==*next(component.begin(),i)){
        if(host>arr5[j]){
        host=arr5[j];
        }
    }
}
minweight+=host;
}
cout<<minweight<<endl;
}
};
void solve(){
 int n,x;
 cin>>n>>x;
 for(int i=1;i<n+1;i++){
    cin>>arr5[i];
 }
 vector<vector<int>>arr;
 for(int i=0;i<x;i++){
        int a,b,c;
 cin>>a>>b>>c;
 if(c>arr5[a]&&arr5[b]<c) {}
 else arr.push_back({c,a,b});
    }
    mst ab(n);
 ab.getmst(arr);
}
int main(){
    solve();
}
```
</details>

     </details>
     
# Single Source Shortest Path

# Problems


