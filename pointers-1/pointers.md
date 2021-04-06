# Pointers

## How Machine Store Things 

Main memory divided into bytes, a byte stores 8-bits of information 

Each byte has a unique address, represented by a 64-bits long `unsigned long` \(64bit machine\) in hexadecimal 

Each variable occupies one or more variable and the address of the first byte is the address of that variable 

## Pointer Variables 

The addresses are not stored by `unsigned long`, but **pointer variables**

### Declaring A Pointer Variable 

**FORM `int *p;`**

Declare a pointer variable: "`p` is a pointer to an `int` object \(or, `int` type pointer\)", and `p` represents a memory address

## Operations On Pointers

### Operators For Use With Pointers 

1. **`&` \(address operator\): Getting the address** of a variable
2. **`*` \(indirection operator\): Getting the value** stored in an address \(the object pointed to by a pointer\)

Example of using two operators 

```c
int i, *ptr1;
ptr1 = &i; 
int *ptr2 = &i; // the `*` is not a indirection operator, but a indication of ptr
```

Caution:

* A declared pointer is not automatically initialized \(`p` does not have a value yet\)
* While not initialized, cannot access the value of the pointer nor assign value to it
* Wrong example:

  ```c
  int *p;
  *p = 1 // wrong, don't know where p is pointing, so cannot assign value
  ```

### Pointer Variable and Pointer Constant 

In the above example, `ptr1` and `ptr2` are  **pointer** **variables**, of which the value can be changed 

`&i` is a **pointer** **constant**, at the time `i` is declared, the address is fixed by the machine, so `&i` cannot be used for an lvalue. Wrong example:

```c
&i = p; // illegal
```

### Pointer Assignment 

#### Copy Address 

**FORM `p = q; // suppose p and q are two pointers`** 

Copies the value of pointer variable into another pointer variable

Then two pointer variables have the same address and the indirection are always the same 

#### Copy Content 

**FORM** **`*p = *q; // suppose p and q are two pointers`**

Only copies the content of the object pointed by `q` into the object pointed by `p`, 

`p`, `q` are not necessarily point to the same address 



## Pointers And Arrays

### Pointer And 1-Dimensional Array

A pointer can point to an array element, examples:

```c
int a[10], *p, *q;
p = a;     // points to the first element of array a
q = &a[8]; // points to the eigth element of array a 
*q = 5;    // try to assgin 5 to a[8]
```

#### Pointer Arithmetic \(Array Exclusive\) 

There are three advanced arithmetic operations on pointers, the variables must point to elements of the same array

1. Adding An Integer 
2. Subtracting An Integer
3. Subtracting One Pointer From Another 

Example:

```c
p = &a[i];  // p points to a[i]    
q = p + 3;  // q points to a[i+3], or 3 memory unit (12B) after a[i]
p += 6;     // p points to a[i+6]
printf("%d", p-q); // same as 6 - 3, output is 3
if (p >= q) {...}  // can be used for comparsion as well
```

#### Pointer For Array Processing 

**FORM \(by an example\)**

```c
int a[10], *p, sum;
// for loop
sum = 0;
for (p = &a[0]; p < &a[10]; p++)
    sum += *p;
    
// while loop
sum = 0;
p = &a[0]; 
while (p < &a[10]) 
    sum + =*p;
```

Explain: 

* `controlling-expr`
  * `a[10]` does not exist. Using `&a[10]` \(address of a\[10\], address of the memory unit after `a[9]` in `controlling-expr` is okay
  * Attempting to get the `a[10]` will result a segmentation fault
* `finishing-expr`
  * `p++` increment p to next element, for example, from `a[0]` to `a[1]`

### Pointer And 2-Dimensional Array

Recall: 2-dimensional array is stored as a row-major order, so pointers treat a 2-dimensional array as a sequence of 1-dimensional arrays, example:

```c
int a[10][20], *p, *q;
int row, col;
p = &a[0][0]; // p points to the first element
q = p + 15;   // q points to a[0][15]
q = p + 25;   // q points to a[1][5]
// a[10][20] is regarded as a 1-dimensional array of 10-elements
// each element is an array (1-dimensional, of length 20)
```

#### Assign Pointers to Array Elements 

If declaring `int *p;`

* It is valid to assign `p = &a[i][0];` , `p = a[i];`, these means `p` points to the ith row, the first column 
* It is invalid to assign `p = a;`, try to let `p` points to the first row, but which column

If declaring `int (*p)[20];`, declares `p` as an array of 20 type `int` pointers 

* It is valid to assign `p = a;`, `p = &a[0];`, these means `p` points to the first row, the first column
* If advance `p`, ie. `p++;`, this advance `p` to the next row
* `(*p)[0]` \(parentheses determines the precedence of evaluation, so essential\) now points to the second row, the first column 

If declaring `int **q;`, declares `p` as a pointer to a pointer

* It is valid to assign `q = a;` , which has the same effect using `p` as an array of 20 type `int` pointers, but the compiler will throw a warning 

### Pointer And Variable-Length Array \(VLA\)

Pointers are allowed to points to elements of a variable-length array \(VLA\) for both 1-dimensional array and 2-dimensional array 

Example of a 1-dimensional array

```c
void f(int n) {
    int a[n], *p;
    p = a;         // the same p = &a[0]
}
```

Example of a 2-dimensional array

```c
void f(int m, int n) {
    int a[m][n], (*p)[k]; // p is a pointer to a type int array of length k (== n)
    p = a;         // the same as p = &a[0]
```

