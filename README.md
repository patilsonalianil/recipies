// C program for RSA asymmetric cryptographic
// algorithm. For demonstration values are
// relatively small compared to practical
// application
// #include<stdio.h>

#include <iostream>
#include <bits/stdc++.h>
#include <cmath>
using namespace std;

// Returns gcd of a and b
int gcd(int a, int h)
{
int temp;
while (1)
{
temp = a%h;
if (temp == 0)
return h;
a = h;
h = temp;
}
}

// Code to demonstrate RSA algorithm
int main()
{
// Two random prime numbers
double p = 3;
double q = 7;

// First part of public key:
double n = p*q;

// Finding other part of public key.
// e stands for encrypt
double e = 2;
double phi = (p-1)*(q-1);
while (e < phi)
{
// e must be co-prime to phi and
// smaller than phi.
if (gcd(e, phi)==1)
break;
else
e++;
}

// Private key (d stands for decrypt)
// choosing d such that it satisfies
// d*e = 1 + k * totient
int k = 2; // A constant value
double d = (1 + (k*phi))/e;

// Message to be encrypted
double msg = 20;

cout<<"message="<<msg;

// Encryption c = (msg ^ e) % n
double c = pow(msg, e);
c = fmod(c, n);
cout<<" \nEncrypted data ="<<c;

// Decryption m = (c ^ d) % n
double m = pow(c, d);
m = fmod(m, n);
cout<<"\nOriginal Message Sent = "<<m;

return 0;
}
----------------------------------------------------------------------------------------------------------------------------------------------------------
//Diffie
#include <iostream>
using namespace std;

// Function to compute a^m mod n
int compute(int a, int m, int n)
{
int r;
int y = 1;

while (m > 0)
{
r = m % 2;

// fast exponention
if (r == 1)
y = (y*a) % n;
a = a*a % n;

m = m / 2;
}

return y;
}

// Cpp program to demonstrate Diffie-Hellman algorithm
int main()
{
int p = 23; // modulus
int g = 5; // base

int a, b; // a - Alice's Secret Key, b - Bob's Secret Key.
int A, B; // A - Alice's Public Key, B - Bob's Public Key

// choose secret integer for Alice's Pivate Key (only known to Alice)
a = 6; // or use rand()

// Calculate Alice's Public Key (Alice will send A to Bob)
A = compute(g, a, p);

// choose secret integer for Bob's Pivate Key (only known to Bob)
b = 15; // or use rand()

// Calculate Bob's Public Key (Bob will send B to Alice)
B = compute(g, b, p);

// Alice and Bob Exchanges their Public Key A & B with each other

// Find Secret key
int keyA = compute(B, a, p);
int keyB = compute(A, b, p);

cout<<"Alice's Secret Key is " << keyA;
cout<<"\nBob's Secret Key is "<<keyB;

return 0;
}
