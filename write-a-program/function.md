# Functions

## `main()`, Starting Point Of A Program

* **FORM `int main(void) {...}` OR `int main(int argc, char *argv[]) {...}`**

## Defining Functions

* **FROM `return-type func-name(parameters) {...}`**
* Example:

  ```c
  double average(double a, double b) {
      return (a + b) / 2;
  }
  ```

* Analyze the example:
  * Each time `average()` is called, a value typed `double` will be returned 
  * Parameter `a`, `b` are supplied when the function is called
  * Parameters' type are declared respectively even if their types are the same
  * `return` return the value, but using the value or not depend on the caller 

### Sequential Trait In C Compilation 

* C is compiled sequentially, so the compiler must know what the function is before using it
* Solving in two ways:

  * The function defined before it is called
  * Give a function declaration \(prototype\) before `main()`, give function definition after `main()`
    * **FORM `return-type func-name(parameters);`**
    * This way is preferred
    * In function declaration \(prototype\), the parameter variable names can be omitted

## Function Termination 

### `return`

**FORM `return expr;`**

* Non-`void` function should have a return, otherwise, cause an error
* The returned type must match or implicit conversion happens 
* Status code of return \(applied to `main()`\)
  * `0`: terminates normally
  * `-1`: terminates with an error
* The returned value may not be useful all the time 
  * Example: the `printf()`'s returned value is seldom used 
  * Sometimes, people put `(void)` \(a casting\) t show that the returned value is discarded 
  * Example: 

    ```c
    (void)printf("I don't need the returned value");
    ```

#### Special Note of Returning A Pointer

* No pointer to an automatic local variable can be returned, since that local variable won't exist if exit the function 

  ```c
  int* f(void){
      int i, *ptr;
      ptr = &i;
      ...
      return ptr; // wrong, i's address is deleted and memory storing i 
                  // is deallocated after function terminates
  }
  ```

### `exit()` Function

* **FORM `exit(status-code);`**
* Terminates the program permanently 
* `#include <stdlib.h>` required, it's a function from that header file 
* The status-code is usually replaced by a macro definition
  * In `stdlib.h`, there is `EXIT_SUCCESS` \(`0`\) and `EXIT_FAILURE` \(`1`\) defined  
  * Or set up a marco definition yourself

## Calling Functions

* **FORM `variable-name = func-name(arguments);`**

### Argument

* The arguments are _passed by value \(exceptions apply\)_, that is, create new copies of the current arguments 

#### Array Arguments

* Array arguments are the exceptions, array names are treated as pointers, no new copies will produce for an array
* So every modification is done on the original array   
* A 1D array can be declared in two ways:
  * `int sum_array1(int a[10]);`
    * Fixed length and cannot be changed during calls
    * The actual length must be greater or equal to 10, but only the first ten elements are used 
  * `int sum_array2(int a[], int len);`
    * 1D array with unknown length
    * The length usually specified by the second parameter, if missing, hard to determine the length
* A 2D array can only have the 1st dimension to be "unknown"
  * `int sum_array3(int a[][100], int n);`
* Variable-length array parameters
  * `int sum_array2(int len, int a[len]); // mind the order`
* `static` to declare the minimal length \(can be only used on the 1st dimension\), the compiler uses it for possible speed up 
  * `int sum_array3(int a[static 10][100], int n); // 1st dimension is >= 10`
* In C99, can create an unnamed array on the fly by specifying elements it contains 
  * `total = sum_array((int[]){3, 0, 3, 4, 1}, 5);`
  * `total = sum_array((int[]){2*i, i+j, j*k}, 3); // use of variables`
* Cannot use `sizeof()` operator to an array in a function call to determine array length

#### Pointer Arguments

* A pointer can be used as arguments, passing an array to a function is an example of a pointer as an argument
* The compiler won't tell the difference if passing a long integer into a function that asks for a pointer, the program will carry out that `long` as the pointer, which will cause an error 

  ```c
  // function defination
  decompose(int, int*, int*);

  // function call 
  long i, d;
  ... // assigning i and d proper long int values
  decompose(3.14159, i, d); // where compiler won't tell t
  ```

* `const` is used to protect the object, it says that the function cannot change the integer that the `ptr` \(pointer\) points to, but not prevent the function from changing the `ptr` \(pointer\) itself. Example:

  ```c
  void f(const int *p) {
       int j;
       *p = 0; // wrong, change the integer that `p` points to
       p = &j; // legal, change the address that `p` points to
  }
  ```



### 





