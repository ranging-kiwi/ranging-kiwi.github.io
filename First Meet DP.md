# The First Clash against Dynamic Programming Feb/24

## How the story begin

In order to have some more meaningful contests to join in, I decided to learn algorithm by my own (without any courses) on this winter vacation. but unfortunately, firstly, I have too many other things to handle which distract my attention, so I have not make much progress in alogorithm learning (I only have C language grammar as my basic knowledge) ; secondly, the book I tried to apply couldn't much perfectly suited my apetite, so I took many detours.  
Now, I choose to learn algorithm and C++ grammar by doing as many competitve programming questions as I can (nevertheless, to keep the learning quality is on the definately first place). I believe, only in this way, can I truly start my journey on competitve programming (btw I loving solving any kind of mathematic questions in middle school, but the mathematical questions in university are so meaningless that I decided to dedicate in competitve programming).

Just to say, the reason why I use such an awful writing skill to record my blog is that I'm trying to make use of all time to training my English. I desperately need to improve my English level.

## Question

This question is come from the *130 questions for the beginners* in **nowcoder tracker** (yes, I still thick I'm so weak for any formal contest, and sure I am).  
noob40:  
This is a two-dimensional Fibonacci sequence:  
a<sub>i</sub><sub>j</sub>=1 i=1,j=1  
a<sub>i</sub><sub>j</sub>=a<sub>i-1</sub><sub>j</sub> i>=2,j=1  
a<sub>i</sub><sub>j</sub>=a<sub>i</sub><sub>j-1</sub> i=1,j>=2  
a<sub>i</sub><sub>j</sub>=a<sub>i-1</sub><sub>j</sub>+a<sub>i</sub><sub>j-1</sub> i>=2,j>=2  
I: Enter two integers n,m, stand for row and column coordinate respectively, 1<=n,m<=10<sup>3</sup>  
O: A number a<sub>i</sub><sub>j</sub>mod(10<sup>9</sup>+7)

## Solution

### False Solution

```
  #include <iostream>
  #include<cmath>
  using namespace std;
  
  long long fibonacci(int n,int m){
      if(n==1&&m==1) return 1;
      if(n>1&&m==1) return fibonacci(n-1,m);
      if(n==1&&m>1) return fibonacci(n,m-1);
      return fibonacci(n-1,m-1);
  }
  
  int main() {
      ios::sync_with_stdio(false);
      cin.tie(0);
      int n,m;
      cin>>n>>m;
      cout<<(fibonacci(n,m))%(7+(int)pow(10,9));
      return 0;
  }
```

Although I use iostream accelerator and have no mistakes in programming, it sill TLE.  
This code is actually doing a m-by-n grid, and the recursive way of computing will finally increasing as a expotential speed.

### Correct Solution

```
  #include<iostream>
  using namespace std;
  
  const int mod=1000000007;
  int dp[1000][1000];
  
  int main(){
      int n,m;
      cin>>n>>m;
      for(int i=1;i<=n;i++){
          for(int j=1;j<=m;j++){
              if(i==1||j==1) dp[i][j]=1;
              else dp[i][j]=(dp[i-1][j]+dp[i][j-1])%mod;
          }
      }
      cout<<dp[n][m];
      return 0;
  }
```

The only feasible path: DP.  
The essence of this question is: How many ways to go from (1,1) to (n,m)?  
And this is the definition of Dynamic Programming: number of unique path in a grid (the formula of DP).  
Dynamic Programming is like a kind of that: pre-traversal all of the datas and record for memoization, and one data comes from function(pre-data).

## Some knowledge need to be added (by AI)

Dynamic Programming three elements:  
1. State definition: something to describe the state, like dp[i][j] stands for the number of path to reach (i,j)  
2. State transition eqution: a connection between to close-related states, from known states to unknown states, like dp[i][j]=dp[i-1][j]+dp[i][j-1]
3. Initial states / boundary conditions

The spriti of DP: a problem can be broken down into a few *overlapping* subproblems, and the solutions to the subproblems can be reused.  
And as long as I use the way of DP, together with memoization, the repeatitive computation can be saved a lot.
