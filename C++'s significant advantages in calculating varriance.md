# C++'s significant advantages in calculating varriance Mar/2

## Background

Sorry for these days disapprearance, cause I was busy with a translation application, adn waiting for dilivering my Raspberry server. Now, the university officially starts, which means I have to allocate my time more properly, to find a space for myself growing (the useless university, the useless classes, the awful roomate, bah). There's no stopping me. I believe I'll moving following my heart.

What drives me crazy is that the preview in github for markdown even doesn't support LaTeX??

That sucks. I'm heading forward my Raspberry...

## Question

Calculate range and varriance.

$s^2=\frac{1}{n} \sum_{i=1}^{n} (a_i-a)^2$

$a=\frac{1}{n} \sum_{i=1}^{n} a_i$

I: one number in the first line: *t*, stands for the number of loop; and the following *2t* lines are divided as 2 lines as a group, first line representing the number of samples *n* and the second line containing the values of the samples  
O: one line for one group of range and varriance, seperated by a space

## Solution

### Normal C-style code:

```
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;
int findmax(int arr[],int n){
    int max=arr[0];
    for(int i=0;i<n;i++){
        if(arr[i]>max) max=arr[i];
    }return max;
}
int findmin(int arr[],int n){
    int min=arr[0];
    for(int i=0;i<n;i++){
        if(arr[i]<min) min=arr[i];
    }return min;
}
void range(int arr[],int n){
    int max=findmax(arr,n);
    int min=findmin(arr,n);
    cout<<max-min<<" ";
}
void variance(int arr[],int n){
    double sum=0.0;
    for(int i=0;i<n;i++){
        sum+=arr[i];
    }
    double avg=sum/n;
    double temp=0.0;
    for(int i=0;i<n;i++){
        temp+=pow(arr[i]-avg,2);
    }
    cout<<fixed<<setprecision(3)<<temp/n<<endl;
}
int main() {
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        int arr[n];
        for(int i=0;i<n;i++){
            cin>>arr[i];
        }
        range(arr,n);
        variance(arr,n);
    }
    return 0;
}
```
Obviously, the C-description is of great length. So we have to unearth the powerful tools in C++

### Advanced C++-style code:

```
#include<iostream>
#include<iomanip>
#include<cmath>
#include<vector>
#include<algorithm>
#include<numeric>
using namespace std;
void solve(){
    int n;
    if(!(cin>>n)) return;
    vector<int> arr(n);
    for(int &x:arr) cin>>x;
    auto [min_it,max_it]=minmax_element(arr.begin(),arr.end());
    cout<<(*max_it-*min_it)<<" ";
    double sum=accumulate(arr.begin(),arr.end(),0.0);
    double avg=sum/n;
    double temp=0.0;
    for(int x:arr){
        temp+=pow(x-avg,2);
    }
    cout<<fixed<<setprecision(3)<<temp/n<<endl;
}
int main(){
    int t;
    cin>>t;
    while(t--){
        solve();
    }
    return 0;
}
```



## Explanation: Useful tools in C++

  for(int &x:arr) cin>>x;
Use **&** to change the true value of arr[i]; Use this kind of syntax to simplify loops

  auto [min_it.max_it]=minmax_element(arr.begin(),arr.end());
structured binding *min_it* and *max_it* because minmax_element return two value in the form of **iterator**. In addition, **min_element** and **max_element** are also available.

  double sum=accumulate(arr.begin(),arr.end(),0.0);
accumullate, from **arr.begin()** to **arr.end()**, and have 0.0 as the initial number
