> This document is out of date. Many informations may not be exact. [Check the latest information in the Simplefied Chinese version](https://github.com/FNatsuka/fstdlib/blob/master/doc/poly.zh-CN.md).

# Poly.h Info.

This is the informations related to poly.h. You can read a better rendered version [here]().


## Fixed Modulo Polynomial

The fixed modulo polynomial use specified integers as its modulo, default 998244353. If you would like to modify the modulo to $P$, you have to ensure:
- $P$ has to be a prime number, and is able to be expressed as $a*2^k+1$, where $a$ and $k$ are postive integer, and $2^k$ is greater always greater than the length of all instances.
- Let $G$ be a [primitive root](https://en.wikipedia.org/wiki/Primitive_root_modulo_n) modulo $P$, you should assign $P$ and $G$ to `fstdlib::mod` and `fstdlib::grt` respectively.

The strict modulo restriction is caused by Number Theoretic Transform (NTT) used to implement the calculation.

To create a fixed modulo polynomial instance, just call for `fstdlib::poly`. You can use the following method to initialize a `fstdlib::poly`:


|Name|Intro.|
|:-:|:-:|
|`poly(std::vector<int>)`|Initialize a polynomial with an vector.|
|`poly(std::size_t n = 0)`|Construct a polynomial of length n, with all elements set to zero.|

Some features are inherit from `std::vector`, like `void resize(std::size_t len, int val = 0)` and `std::size_t size(void)`. You can use it like to a vector.

Several operators are overloaded, some of them are listed in the following form:

|Operator|Intro.|Implement|
|:-:|:-:|:-:|
|`*` and `*=`|Calculate the convolution of two polynomials.|FNTT|
|`+` and `+=`|Calculate the sum of two polynomials.||
|`>>` and `>>=`|Right shift the polynomial.||
|`<<` and `<<=`|Left shift the polynomial.||

Some functions available are listed in the following form:

|Name|Intro.|Implement|
|:-:|:-:|:-:|
|`poly poly::inv(int n)`|Calculate the inverse modulo $x^n$.|Newton's Method|
|`poly log(const poly &)`|Calculate a polynomial $H$, such that $H \equiv \ln F \pmod{x^n}$.|Derivative and Integration|
|`poly exp(const poly &)`|Calculate a polynomial $H$, such that $H \equiv \exp F \pmod{x^n}$.|Newton's Method|
|`poly sqrt(const poly &)`|Calculate a polynomial $H$, such that $H^2 \equiv F \pmod{x^n}$.|Newton's Method|

## Arbitrary Modulo Polynomial

The arbitrary modulo polynomial is totally the same with the fixed one, except it has no modulo restriction, which means you can use any integer as your modulo. However, arbitrary modulo polynomial is significant slower than the fixed modulo polynomial in coefficient factor. Besides, you can not operate nonlinear calculation except convolution if the modulo is not a prime number.

To create a fixed modulo polynomial instance, just call for `fstdlib::m_poly`. You can use the following method to initialize a `fstdlib::m_poly`:

|Name|Intro.|
|:-:|:-:|
|`m_poly(std::vector<int>, int mod = 1e9 + 7)`|Initialize a polynomial with an vector. The modulo value of the polynomial is set to mod initially.|
|`m_poly(std::size_t n = 0, int mod = 1e9 + 7)`|Construct a polynomial of length n, with all elements set to zero. The modulo value of the polynomial is set to mod initially.|

You can always change the modulo value by accessing the member named `mod`. Note that the polynomial's coefficient will not change with the change of `mod`.

