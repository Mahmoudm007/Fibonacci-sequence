

_Fibonacci sequence_
=======
##### Mahmoud Mohamed Ali Ahmed - SEC:2 - BN:22

 
 ![6 9f797a7](https://user-images.githubusercontent.com/101353088/194109720-7954e5ec-2e26-405c-ba4e-d5bbbd8cf43d.jpg)
> ###### I get help from [geeksforgeeks](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)


## **first method**
##### assuming we start from **zero** and ask for **n** from the user, using functions.

~~~c++
#include <iostream>
using namespace std;

int fib(int n)
{
    if (n <= 1)
        return n;
    return fib(n - 1) + fib(n - 2);
}

int main()
{
    int n ;
    cin>>n;
    cout << fib(n);
    getchar();
    return 0;
}
~~~
+ Time Complexity: Exponential.
+ Extra Space: O(n) if we consider the function call stack size, otherwise O(1).

___
## **second method**
 
 Useing Dynamic Programming
 ~~~c++
 
#include<bits/stdc++.h>

using namespace std;

class GFG{

public:
int fib(int n)
{

	int f[n + 2];
	int i;

	
	f[0] = 0;
	f[1] = 1;

	for(i = 2; i <= n; i++)
	{

	f[i] = f[i - 1] + f[i - 2];
	}
	return f[n];
	}
};

int main ()
{
	int n;
	GFG g;
	cin>> n;

	cout << g.fib(n);
	return 0;
}
~~~
+ Time complexity: O(n) for given n
+ space complexity: O(n)

___
## **third method**

~~~c++
#include<bits/stdc++.h>
using namespace std;

int fib(int n)
{
    int a = 0, b = 1, c;
    if( n == 0)
        return a;
    for(int i = 2; i <= n; i++)
    {
       c = a + b;
       a = b;
       b = c;
    }
    return b;
}

int main()
{
    int n;
    cin>>n;

    cout << fib(n);
    return 0;
}
~~~
+ Time Complexity: O(n) 
+ Extra Space: O(1)

___
### *Method 4: Using power of the matrix [(1, 1), (1, 0)]*
##### ![6matrix](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-eee4fa0c08f84de02fd9767ad0206d6c_l3.svg) 

~~~ c++
#include<bits/stdc++.h>
using namespace std;

// Helper function that multiplies 2
// matrices F and M of size 2*2, and
// puts the multiplication result
// back to F[][]
void multiply(int F[2][2], int M[2][2]);

// Helper function that calculates F[][]
// raise to the power n and puts the
// result in F[][]
// Note that this function is designed
// only for fib() and won't work as
// general power function
void power(int F[2][2], int n);

int fib(int n)
{
	int F[2][2] = { { 1, 1 }, { 1, 0 } };
	
	if (n == 0)
		return 0;
		
	power(F, n - 1);
	
	return F[0][0];
}

void multiply(int F[2][2], int M[2][2])
{
	int x = F[0][0] * M[0][0] +
			F[0][1] * M[1][0];
	int y = F[0][0] * M[0][1] +
			F[0][1] * M[1][1];
	int z = F[1][0] * M[0][0] +
			F[1][1] * M[1][0];
	int w = F[1][0] * M[0][1] +
			F[1][1] * M[1][1];
	
	F[0][0] = x;
	F[0][1] = y;
	F[1][0] = z;
	F[1][1] = w;
}

void power(int F[2][2], int n)
{
	int i;
	int M[2][2] = { { 1, 1 }, { 1, 0 } };
	
	// n - 1 times multiply the
	// matrix to [(1,0),(0,1)]
	for(i = 2; i <= n; i++)
		multiply(F, M);
}

// Driver code
int main()
{
	int n = 9;
	
	cout << " " << fib(n);
	
	return 0;
}
~~~
+ Time Complexity: O(n) 
+ Extra Space: O(1)

___

## **Method 5: (Optimized Method 4)**
#### Method 4 can be optimized to work in O(Logn) time complexity. We can do recursive multiplication to get power(M, n)

~~~c++
// Fibonacci Series using Optimized Method
#include <bits/stdc++.h>
using namespace std;

void multiply(int F[2][2], int M[2][2]);
void power(int F[2][2], int n);

// Function that returns nth Fibonacci number
int fib(int n)
{
	int F[2][2] = [(1, 1), (1, 0)];
	if (n == 0)
		return 0;
	power(F, n - 1);

	return F[0][0];
}

// Optimized version of power() in method 4
void power(int F[2][2], int n)
{
	if(n == 0 || n == 1)
	return;
	int M[2][2] = [(1, 1), (1, 0)];
	
	power(F, n / 2);
	multiply(F, F);
	
	if (n % 2 != 0)
		multiply(F, M);
}

void multiply(int F[2][2], int M[2][2])
{
	int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
	int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
	int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
	int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];
	
	F[0][0] = x;
	F[0][1] = y;
	F[1][0] = z;
	F[1][1] = w;
}
int main()
{
	int n = 9;
	
	cout << fib(9);
	getchar();
	
	return 0;
}
~~~
+ Time Complexity: O(Logn) 

+ Extra Space: O(Logn) if we consider the function call stack size, otherwise O(1).

____

## Method 6: (Another approach(Using Binet’s formula))
#### In this method, we directly implement the formula for the nth term in the Fibonacci series. 
Fn = {[(√5 + 1)/2] ^ n} / √5 

>Note: Above Formula gives correct result only upto for n<71. Because as we move forward from n>=71 , rounding error becomes significantly large . Although , using floor function instead of round function will give correct result for n=71 . But after from n=72 , it also fails.

>Example: For N=72 , Correct result is 498454011879264 but above formula gives 498454011879265.  


[Reference:](http://www.maths.surrey.ac.uk/hosted-sites/R.Knott/Fibonacci/fibFormula.html)

~~~c++
// C++ Program to find n'th fibonacci Number
#include<iostream>
#include<cmath>

int fib(int n) {
double phi = (1 + sqrt(5)) / 2;
return round(pow(phi, n) / sqrt(5));
}

// Driver Code
int main ()
{
int n = 9;
std::cout << fib(n) << std::endl;
return 0;
}
~~~

+ Time Complexity: O(logn), this is because calculating phi^n takes logn time
+ Auxiliary Space: O(1)

_____

## *time complexity table*
 
 |    method    |time complexity|
 |-------------:|:-------------:|
 |  method 1    |  Exponential  |
 |  method 2    |  O(n)         |
 |  method 3    |  O(n)         |
 |  meyhod 4    |  O(n)         |
 |  method 5    |  O(Logn)      |
 |  method 6    |  O(Logn)      |
 
 
 
 
