# Natrually Using Vector in Programming for The First Time Feb/24

## A brief statement

Actually, I have done this question yesterday and so as the last dp question, but I was busy handling some tricky problems which emerged when i tried to purchase my first game (red dead redamption II) and frustrated to optimize what platform should i use to start my conmpetitve programming journey by blogging (which is definately stupid) (btw, I find my GitHub text editor *soft wrap* has been trun off? ahhhhhh, that's ridiculous).

But fuck'em all, my top priority now is start learning.

Actually, this is not the first time i come across vector, but all of that past experiences are based on a guiding book or AI assistant.  
So this means i need to supply much vector-knowledge to satisfy my upcoming need.

## Question

This question is come from the *130 question for the beginner* in **nowcoder tracker** as well.  
noob41:  
There is a series of integers。 You need to read the input and reverse it, and then output the result.  
I: input n integers a<sub>1</sub>, a<sub>2</sub>, ... 0 (1<=n<=100) (1<=a<sub>i</sub><=2<sup>31</sup>-1)  
O: output the integers in reversed order (excluding the end sign "0") and separate them wil spaces  

## Solution

```
#include <iostream>
#include<vector>
using namespace std;

int main() {
    vector<long long> number;
    while(1){
        long long n;
        cin>>n;
        if(n==0) break;
        number.push_back(n);
    }
    int length=number.size();
    for(int i=length-1;i>=0;i--){
        cout<<number[i]<<" ";
    }
}
```

Because the number of integer series is unknown, just like unknown length array, and it is absolutely suit for the special vector STL in C++.

## The Basic that must know about vector STL

```
#include<vector>

vector<int> num;  //initialize a empty vector
vector<int> num(10);  //initialize a empty vector has 10 "0" elements
vector<int> num(10,5);  //initialize a vector and set all 10 elements as "5"
vector<int> num={1,2,3,4,5};  //initialize a vector and set all elements, or the "=" can be omitted
vector<int> num(nums);  //copy nums to initialize num
vector<int> num(nums.begin(),num.begin()+3)  //copy nums's first 3 elements to initialize num

vector<vector<int>> num(5);  //initialize a five-row empty 2-D vector
vector<vector<int>> num(5,vector<int>(4));  //initialize a five-row-four-column empty 2-D vector
vector<vector<int>> num(5,vector<int>(4,1));  //initialize a five-row-four-column 2-D vector and set all elements as "1"

int n=num[i];  //get the "i"th element (not check if supass the boundary)
int n=num.at(i);  //get the "i"th element (check if surpass the boundary)
int n=num.front();  //get the first element
int n=num.back();  //get the last element
int *pt=num.data();  //get the pointer point at the first element
int length=num.size();  //get the size/length of vector
int capacity=num.capacity();  //show the arranged size/length that can be filled
bool isEmpty=num.empty();  //if empty, return true; if not empty, return false
num.resize(n);  //revise the size of vector, the new elements will be set as "0"; the overflowed elements wil be abandoned

num.push_back(10);  //add the element "10" at the end of the vector
num.pop_back();  //delete the last element of the vector
num.insert(num.begin()+2,1);  //insert "1" at the position "2", and all elements after the insertion position will be shift to the right
num.insert(num.begin()+2,3,1);  //insert 3 "1"s at the position "2"
num.insert(num.end(),nums.begin(),nums.end());  //insert nums at the end of num
num.emplace(num.begin()+2,1);  //same as insert, but more effective, only in C++11
num.assign(nums.begin(),nums.end());  //clear num, and insert elements from nums

num.erase(num.begin()+2);  //delete the position and the value at "2"
num.erase(num.begin()+1,num.begin()+3);  //delete the interval from the position "1" to "3"
num.clear();  //set the vector empty

#include<algotithm>
sort(num.begin(),num.end());
sort(num.begin(),num.end(),greater<int>());
reverse(num.begin(),num.end());
auto pt=find(num.begin(),num.end(),1);
bool binary_search(num.begin(),num.end(),1);
auto maxpt=max_element(num.begin(),num.end());
auto minpt=min_element(num.begin(),num.end());
int cnt=count(num.begin(),num.end(),1);
sort(num.begin(),num.end()); auto last=unique(num.begin(),num.end()); num.erase(last,num.end());
```
