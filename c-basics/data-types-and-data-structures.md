---
description: 'In this section: 1) int, 2) float, 3) char, and 4) _bool'
---

# Data Types \(Scalar\)

The common data types in C are **integer**, **float**, **character**, they are held by scalar variables 

## Integer 

Integers are always stored in **binary**, regardless of what notation we've used to express them

### Base 10 \(decimal\)

* `int` can have singed and unsigned
* The default `int` a is 32-bits long binary representation
* There are short, short short, long, long long for both signed and unsigned integers, which has length 8 bits, 16 bits, 32/64 bits \(depend on the machine\), and 64bit respectively
* Negative values are two's complement 

### Base 8 \(Octal\)

* Default signed, but no way to print negative directly, and cannot change to unsigned
* Must begin with a zero 
* Example: `017`, `0377`, `07777`

### Base 16 \(Hexadecimal\)

* Default signed, but no way to print negative directly, and cannot change to unsigned
* Must begin with `0x`
* Example: `0x17`, `0xff`, `0x7fff`

##  Floating Types

Using "[the IEEE standard 754](https://www.h-schmidt.net/FloatConverter/IEEE754.html)", no matter `float`, `double`, or `long double`, they are all binary exponential format

### `float`

* Single-precision
* Signed 4-bytes/32-bits long

### `double`

* Double-precision
* Signed 8-bytes/64-bits long 

### `long double`

* Extended-precision
* Signed 80-bits or 128 bits long 

## Character 

* `char` is an 8-bits long binary representation 
* The signedness `char` is not specified unless by a programmer 
* In C, [ASCII table ](http://www.asciitable.com/)is used and `char` can be converted to a short short int at all times 

## \_Bool \(in c99\)

* Boolean is an integer type, has only two possible values 0 and 1 \(non-zero\)
* Need `#include <stdbool.h>` to provides a macro `bool` for \_Bool 
  * The macro has `true` and `false` standing for `1` and `0` respectively 

## 



