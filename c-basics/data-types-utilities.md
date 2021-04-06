---
description: >-
  In this section: 1) type conversion (implicit conversion and casting), and 2)
  sizeof() operator
---

# Data Types Utilities

## Type Conversion

### Implicit Conversion \(Promotion\)

* Converting the operand of the narrower type to the type of the other operand \(happen automatically\)
* From narrowest to widest: bool -&gt; char -&gt; short int -&gt; int -&gt; unsigned int -&gt; long int -&gt; unsigned long int -&gt; float -&gt; double -&gt; long double 
* The situations of happening:
  * Operands in arithmetic/logical expression not of the same type
  * Type of right side of an assignment not matching the type of the variable on left side 
  * Type of argument in a function not matching that of parameter
  * Type of function return value not matching the return type

### Casting 

* **FORM `(type-name) expr`**
* `(type-name)` is considered as a unary operator 
* Exists because sometimes implicit conversion \(promotion\) would be problematic 

#### Use Casting To Avoid Overflow 

* Example of overflow \(block 1\), how to solve it by casting \(block 2\), and a wrong solution \(block 3\)

  ```c
  long i;
  int j = 1000;
  // block 1
  i = j * j          // the value is 1000000, will cause overflow 

  // block 2
  i = (long) j * j   // cast the first j to long, 
                     // and implicit conversion will convert the second j

  // block 3
  i = (long) (j * j) // will won't work, the overflow would already 
                     // occurd by the time of cast 
  ```

## `sizeof()` Operator 

* **FORM `sizeof(type-name)`, RETURN `size_t`** 
* This is considered as a unary operator
* The return value ask us to use `%lu` or `%PRIu64` for formatting output 
* Example:

  ```c
  int i;
  printf("Size: %lu\n", sizeof(i));
  ```



