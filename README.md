# DSA-2-Problem-Collection

>You will find some of the topic wise question to practice here.These question can be solved by others way/algorithm too.But i try to gather these problem with those particular topic to practice.All of my solution follows a general structure for that specific topic.you will have idea where i made those change in algorithm.But i encourage to try by yourself first.Thank you and happy coding.

# Contents

## [Minimum Spanning Tree](#Problems)
## [Single Source Shortest Path](#Problems)
## [All Pair Shortest Path](#Problems)
## [Max Flow](#Problems)

# Minimum Spanning Tree
# Problems
<details>
<summary>See Here</summary>
    
# Problem 1

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

# Problem 2
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

# Problem 3
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
            
# Problem 4
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

# Problem 5

>5)Your job is to establish an efficient water supply network for every residence within a
city. Let us conceptualize this city as a 2D plane, where each house is positioned using
coordinates. You are provided with an array, named 'houses,' representing the
coordinates of houses in the city, denoted as houses[i] = [xi, yi]. The required pipe to
connect two houses, [xi, yi] and [xj, yj], is determined by the Manhattan distance
between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.
Your objective is to calculate the minimum cost needed to connect all houses for an
efficient water supply. All houses are considered connected if there exists exactly one
simple path between any two houses.
Assuming all distances are measured in kilometers, the cost for purchasing each kilometer of
pipe is 1 taka.
  
Input<br>

The first input line contains one integer n, representing the number of houses. Following
that, there are n lines describing the house positions. Each line consists of two integers,
x and y, where x and y represent the two coordinates of the house position

Output<br>

Print the minimum cost of establishing such a pipeline.

Example:<br>

|Input|output|
|--|--|
5
|0 0  |20|
2 2
3 10
5 2
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
int getmst(vector<vector<int>>arr,int del,int take){
    minweight=0;
    unionfined x(k);
    if(take!=-1){
        x.unionset(arr[take][1],arr[take][2]);
        minweight+=arr[take][0];
    }
for(int i=0;i<arr.size();i++){
        if(i!=del){
        int start=x.Findparent(arr[i][1]);
        int finish=x.Findparent(arr[i][2]);
     if(start!=finish){
            minweight+=arr[i][0];
        x.unionset(start,finish);
     }
}
}
for(int i=0;i<k;i++){
    if(x.Findparent(i)!=x.Findparent(0)){
        return INT_MAX;
    }
}
return minweight;
}
};
void check(int n){

    vector<vector<int>>arr;
for(int i=0;i<n;i++){
    int x,y,z;
    cin>>x>>y;
    arr.push_back({x,y,i});
}
vector<vector<int>>arr2;
for(int i=0;i<n;i++){
    for(int j=0;j<n;j++){
        if(j!=i){
            int val=abs(arr[i][0]-arr[j][0])+abs(arr[i][1]-arr[j][1]);
            arr2.push_back({val,i,j});
        }
    }
}
sort(arr2.begin(),arr2.end());

    mst a(n);
int weight=a.getmst(arr2,-1,-1);
cout<<weight<<endl;
}
int main(){
 int n;
 cin>>n;
 check(n);

}
```
</details>
     </details>

# Single Source Shortest Path
# Problems
<details>
<summary>See Here</summary>
    
# Problem 1
>1)I am going to my home. There are many cities and many bi-directional roads between them. The cities are numbered from 0 to n-1 and each road has a cost. There are m roads.
You are given the number of my city t where I belong.
Now from each city you have to find the minimum cost to go to my city. The cost is defined by the cost of the maximum road you have used to go to my city.

Original Link:https://lightoj.com/problem/country-roads
<details>
<summary>Solution</summary>
    
```cpp
#include<bits/stdc++.h>
using namespace std;
void dijkstra(vector<pair<int,int>>*graph,int num,int source){
vector<int>visited(num,0);
priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>Q;
vector<int>dist(num,INT_MAX);
 Q.push({0,source});
 dist[source]=0;
 while(!Q.empty()){
int u=Q.top().second;
Q.pop();
    for(auto a:graph[u]){
            if(a.first>=dist[u]){
                     if(dist[a.second]>a.first){
                dist[a.second]=a.first;
                Q.push({dist[a.second],a.second});
    }
}
else{
     if(dist[a.second]>dist[u]){
                dist[a.second]=dist[u];
                Q.push({dist[a.second],a.second});
    }
}
}
 }
 for(int i=0;i<num;i++){
    if(dist[i]!=INT_MAX)cout<<dist[i]<<endl;
    else cout<<"Impossible"<<endl;
 }
}
void solve(){
  int n,m;
cin>>n>>m;
vector<pair<int,int>>graph[n];
for(int i=0;i<m;i++){
    int x,y,z;
    cin>>x>>y>>z;
    graph[x].push_back({z,y});
    graph[y].push_back({z,x});
}
int source;
cin>>source;
dijkstra(graph,n,source);


}
int main(){
  int n;
  cin>>n;
  int i=1;
  while (n--){
        cout<<"Case "<<i<< ":"<<endl;
        i++;
    solve();
  }
}
```
</details>

# Problem 2
>2)Tanvir returned home from the contest and got angry after seeing his room dusty. Who likes to see a dusty room after a mind boggling programming contest? After checking a bit he found that there is no brush in him room. So, he called Atiq to get a brush. But as usual Atiq refused to come. So, Tanvir decided to go to Atiq's house.
The city they live in is divided by some junctions. The junctions are connected by two way roads. They live in different junctions. And they can go to one junction to using the given roads only.
Now you are given the map of the city and the distances of the roads. You have to find the minimum distance Tanvir has to travel to reach Atiq's house.

Original link:https://lightoj.com/problem/brush-5
<details>
<summary>Solution</summary>
    
```cpp
    #include<bits/stdc++.h>
using namespace std;
void dijkstra(vector<pair<int,int>>*graph,int num,int source,int dest){
vector<int>visited(num,0);
priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>Q;
vector<int>dist(num,INT_MAX);
 Q.push({0,source});
 dist[source]=0;
 while(!Q.empty()){
int u=Q.top().second;
Q.pop();
    for(auto a:graph[u]){
            if(dist[a.second]>a.first+dist[u]){
                dist[a.second]=a.first+dist[u];
                Q.push({dist[a.second],a.second});
    }
}
 }

if(dist[dest]!=INT_MAX)cout<<dist[dest]<<endl;
else cout<<"Impossible"<<endl;
}
void solve(){
int n,m;
cin>>n>>m;
vector<pair<int,int>>graph[n+1];
for(int i=0;i<m;i++){
    int x,y,z;
    cin>>x>>y>>z;
    graph[x].push_back({z,y});
    graph[y].push_back({z,x});
}
dijkstra(graph,n+1,1,n);

}
int main(){
int n;
cin>>n;
int i=1;
while(n--){
        cout<<"Case "<<i<<":";
     i++;
    solve();
}
}
  ```
</details>

# Problem 3
>3)Dhaka city is getting crowded and noisy everyday. Certain roads always remain blocked for congestion. In order to convince people avoid shortest routes as it's the number one reason for roads crowded; the city authority has come up with a new plan.
Each junction of the city is marked with a positive integer (≤ 20) denoting the busy-ness of the junction. Whenever someone goes from one junction (the source junction) to another (the destination junction), the city authority gets an amount of money (busy-ness of destination - busy-ness of source)3 (that means the cube of the difference) from the traveler.
Now, the authority has appointed you to find the minimum total amount that can be earned when someone goes from a certain junction (the zero point) to several others.

Original source:https://lightoj.com/problem/extended-traffic
<details>
<summary>Solution</summary>
    
```cpp
#include<bits/stdc++.h>
using namespace std;
void dijkstra(vector<pair<int,int>>*graph,int num,int source,int dest){
vector<int>visited(num,0);
priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>Q;
vector<int>dist(num,INT_MAX);
 Q.push({0,source});
 dist[source]=0;
 while(!Q.empty()){
int u=Q.top().second;
Q.pop();
    for(auto a:graph[u]){
            if(dist[a.second]>a.first+dist[u]){
                dist[a.second]=a.first+dist[u];
                Q.push({dist[a.second],a.second});
    }
}
 }
int x;
cin>>x;
for(int i=0;i<x;i++){
    int y;
    cin>>y;
    if(dist[y]>=3)cout<<dist[y]<<endl;
    else cout<<"?"<<endl;
}
}
void solve(){
int n,m;
cin>>n;
vector<int>arr(n+1);
for(int i=1;i<=n;i++){
    int x;
    cin>>x;
    arr[i]=x;
}
cin>>m;
vector<pair<int,int>>graph[n+1];
for(int i=0;i<m;i++){
    int x,y,z;
    cin>>x>>y;
    z=(arr[y]-arr[x])*(arr[y]-arr[x])*(arr[y]-arr[x]);
    graph[x].push_back({z,y});
}
dijkstra(graph,n+1,1,n);

}
int main(){
int n;
cin>>n;
int i=1;
while(n--){
        cout<<"Case "<<i<<":"<<endl;
     i++;
    solve();
}
}
```
</details>

# Problem 4
>4)In your country there are 𝑁 cities numbered from 1 to 𝑁. You live in city 1. You want to go to city 𝑁.
There are 𝑀 bidirectional roads connecting some cities to each other. It is possible to get to any city from
any other city. But each city has a predefined amount of tax that you have to pay if you enter into that city.
How can you get to city 𝑁 paying the least tax?

Input:<br>
The first line of input contains two integers 𝑁 and 𝑀 – denoting the number of cities and the number of
roads respectively.
The next line contains 𝑁 positive integer values – the tax you need to pay to enter into each city.
The next 𝑀 lines contain two integers 𝑢, 𝑣 (1 ≤ 𝑢, 𝑣 ≤ 𝑁) – denoting that there is a road between city 𝑢
and city v.

Output<br>
Print one integer – the least amount of tax you need to pay to get to city 𝑁.

Example 1:<br>
|Input|output|
|--|--|
3 2
|5 10 15|25|
1 2
2 3

Example 2:<br>
|Input|output|
|--|--|
6 9
|5 5 15 10 10 7|22|
1  2
2  3
3  5
5  4
4  1
2  4
2  5
5  6
3  6
<details>
<summary>Solution</summary>
    
```cpp
    
#include<bits/stdc++.h>
using namespace std;
void dijkstra(vector<pair<int,int>>*graph,int num){
vector<int>visited(num,0);
priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>Q;
vector<int>dist(num,INT_MAX);
 Q.push({0,1});
 dist[1]=0;
 while(!Q.empty()){
int u=Q.top().second;
Q.pop();
    for(auto a:graph[u]){
            if(dist[a.second]>a.first+dist[u]){
                dist[a.second]=a.first+dist[u];
                Q.push({dist[a.second],a.second});
    }
}
 }
 cout<<dist[num-1]<<endl;
}
int main(){
    int n,m;
cin>>n>>m;
vector<int>cost(n+1);
for(int i=1;i<=n;i++){
    int x;
    cin>>x;
    cost[i]=x;
}
vector<pair<int,int>>graph[n+1];
for(int i=0;i<m;i++){
    int x,y;
    cin>>x>>y;
    graph[x].push_back({cost[y],y});
    graph[y].push_back({cost[x],x});
}
dijkstra(graph,n+1);
}

```
    
</details>
</details>

# All Pair Shortest Path
# Problems
<details>
<summary>See Here</summary>
</details>



# Max Flow
# Problems
<details>
<summary>See Here</summary>
</details>

# Problem 1
>1)On the Internet, machines (nodes) are richly interconnected, and many paths may exist between a given pair of nodes. The total message-carrying capacity (bandwidth) between two given nodes is the maximal amount of data per unit time that can be transmitted from one node to the other. Using a technique called packet switching; this data can be transmitted along several paths at the same time.
For example, the figure shows a network with four nodes (shown as circles), with a total of five connections among them. Every connection is labeled with a bandwidth that represents its data-carrying capacity per unit time.
In our example, the bandwidth between node 1 and node 4 is 25, which might be thought of as the sum of the bandwidths 10 along the path 1-2-4, 10 along the path 1-3-4, and 5 along the path 1-2-3-4. No other combination of paths between nodes 1 and 4 provides a larger bandwidth.
You must write a program that computes the bandwidth between two given nodes in a network, given the individual bandwidths of all the connections in the network. In this problem, assume that the bandwidth of a connection is always the same in both directions (which is not necessarily true in the real world).

Original source:https://lightoj.com/problem/internet-bandwidth
<details>
<summary>Solution</summary>
    
```cpp
#include<bits/stdc++.h>
using namespace std;
#define N 10000
int resgraph[N][N];
int graph[N][N];
bool bfs(int s,int t,int n,int parent[N]){
bool vis[n];
memset(vis,0,sizeof(vis));
queue<int>q;
q.push(s);
vis[s]=true;
parent[s]=-1;
while(!q.empty()){
    int u=q.front();
    q.pop();
    for(int i=0;i<n;i++){
        if(vis[i]==0&&resgraph[u][i]>0){
                if(i==t){
                    parent[i]=u;
                    return true;
                }
        q.push(i);
        vis[i]=1;
        parent[i]=u;
        }
    }
}
return false;
}
int ford_fulkerson(int n,int s,int t){
int parent[n];
for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
    resgraph[i][j]=graph[i][j];
}
}
int flow=0;
while(bfs(s,t,n,parent)){
    int low=INT_MAX;
    for(int i=t;i!=s;i=parent[i]){
        int u=parent[i];
        low=min(low,resgraph[u][i]);
    }
     for(int i=t;i!=s;i=parent[i]){
        int u=parent[i];
        resgraph[u][i]-=low;
        resgraph[i][u]+=low;
    }
    flow+=low;
}
return flow;
}

int main(){
    int li;
    cin>>li;
    int k=1;
    while(li--){
int n,m;
cin>>n;
int s,t;
cin>>s>>t>>m;
for(int i=0;i<=n;i++){
    for(int j=0;j<=n;j++){
        graph[i][j]=0;
    }
}
for(int i=0;i<m;i++){
    int x,y,z;
    cin>>x>>y>>z;
    graph[x][y]+=z;
    graph[y][x]+=z;
}
cout<<"Case "<<k<<": "<<ford_fulkerson(n+1,s,t)<<endl;
k++;}
}

```
<\details>
