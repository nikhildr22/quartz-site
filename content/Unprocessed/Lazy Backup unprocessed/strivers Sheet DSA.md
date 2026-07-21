# Pattern programs
https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/


# to print odd numbers
`2*i+1`

# use proper variable names for better understanding during coding interviews
```cpp
void printTriangle(int n) {
        int stars;
        for(int row=1;row<=2*n-1;row++){
            stars = row>n?2*n-row:row;
            for(int star=0;star<stars;star++){
                cout<<"* ";
            }
            cout<<endl;
        }
        
    }
//* 
//* * 
//* * * 
//* * * * 
//* * * * *
//* * * *
//* * *
//* *
//*
```


# print A-Z

```cpp
#include <iostream>
using namespace std;

int main()
{
    for (char c = 'A'; c <= 'Z'; c++)
    {
        cout << c << ' ';
    }
}
```


# C++ STL
[[cpp STL]]