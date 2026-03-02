# A Large Fibonacci Series Feb/26

## Question:

The definition of Fibonacci series:   
f<sub>1</sub>=1, f<sub>2</sub>=1, f<sub>n</sub>=f<sub>n-1</sub>+f<sub>n-2</sub> (n>=3)  
I: enter an integer k on one line (1<=k<=10<sup>6</sup>)  
O: show the answer of f<sub>k</sub>mod(10<sup>9</sup>+7)  

## Analyse:

Considering 1<=k<=10<sup>6</sup>, firstly, the `long long` data type can't hold the expotentially large results; secondly, recursive algorithm can't work, which means there will be a stack overflow and a large aount of repetitive calculation.

Then, here comes the **Dynamic Programming** algorithm and the **modular arithmatic**.

- Dynamic Programming can reduce the number of calculation by memorizing each result when it was calculated out, reducing the time to calculate and the space to store stack.
- Modular arithmatic can cut down the surprisingly large number effectively. And according to the principle of madular arithmatic, (a+b)mod(m)=((a)mod(m)+(b)mod(m))mod(m), there won't be any mathemetical mistakes on the result.
And going further, since what we need to figure out is only the f<sub>k</sub> as a result, we can use iteration to improve the efficiency of Dynamic Programming, by only rolling the three variables we need in one calculation loop, reducing the calculation complexity from O(2<sup>k</sup>) to O(k).

There exists even another algorithmic approach to solve this problem.

**Matrix Exponentiation.**

We can write the recursive relationship in Fibonacci series as **Matrix Mutiplication**, in mathematical language:

(a row of matrix mutiplication is omitted here)  
(and a row of matrix exponentiation is omitted here)

Utilizing binary exponentiation of matrices, the complexity reduce to O(k) to O(log<sub>2</sub> k).

## Solution:

Dynamic Porgramming:
```
#include <iostream>
using namespace std;
int main(){
    int k;
    cin>>k;
    const int mod=1000000007;
    long long a=1;
    long long b=1;
    long long res=0;
    for(int i=3;i<=k;i++){
        res=a%mod+b%mod;
        a=b;
        b=res;
    }
    cout<<res%mod;
    return 0;
}
```

Matrix Exponentiation:
```
#include<iostream>
using namespace std;
const int mod=1000000007;
struct Matrix{
    long long entry[2][2];
    Matrix(){
        entry[0][0]=entry[0][1]=entry[1][0]=entry[1][1]=0;
    }
};
Matrix mutiplication(Matrix A,Matrix B){
    Matrix C;
    for(int i=0;i<2;i++){
        for(int j=0;j<2;j++){
            for(int k=0;k<2;k++){
                C.entry[i][j]=(C.entry[i][j]+A.entry[i][k]*B.entry[k][j])%mod;
            }
        }
    }
    return C;
}
Matrix power(Matrix A,int p){
    Matrix res;
    res.entry[0][0]=res.entry[1][1]=1;
    res.entry[0][1]=res.entry[1][0]=0;
    while(p>0){
        if(p%2!=0) res=mutiplication(res,A);
        A=mutiplication(A,A);
        p/=2;
    }
    return res;
}
int main(){
    int k;
    cin>>k;
    if(k<=2){
        cout<<1;
        return 0;
    }
    Matrix T;
    T.entry[0][0]=T.entry[0][1]=T.entry[1][0]=1;
    T.entry[1][1]=0;
    Matrix res=power(T,k-1);
    cout<<res.entry[0][0];
    return 0;
}
```
