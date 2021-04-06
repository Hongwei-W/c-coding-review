# Dynamic Storage Allocation

Declare a pointer pointing to nowhere at declaration, and the memory location pointed to will be allocated using functions in `<stdlib.h>`. These functions are:

`void *malloc(size_t size);               // allocates a block of memory, no initialization`

`void *calloc(size_t nmemb, size_t size); // allocates a block of memory, clears it`

`void *realloc(void *ptr, size_t size);   // resizes a previously allocated block of memory`

It is up to the programmer to check if the return success or fail. The functions return a generic pointer pointing to the memory block or return a null pointer if the allocation fails. 

The memory allocated has a permanent life span. So, the programmer needs to free it in time in case of running out of memory, and **free** it before the program terminates to **prevent a memory leak.** 

## Allocation Functions

#### `malloc()`

`malloc`\(\) allocates a block of `size` \(in bytes\) without cleaning, this means the memory block could contain garbage value. 

#### `calloc()`

`calloc()` allocates a block of memory by specifying the unit size of your instance and the number of your instances. The memory is cleared with 0 in all bits.

#### `realloc()`

`realloc()` resizes the memory block that is previously allocated using `malloc()`, `calloc()`, or `realloc()`. Memory that is not allocated by these functions could not be reallocated using `realloc()`.

`realloc()` can do the same as `malloc()`, and can do the same as `free()`, illustrates by an example:

```c
a = realloc(null, 2*n*sizeof(int)); // the same as malloc()
a = realloc(a, 0);                  // frees the memory 
```

Example of dynamically allocating storage for an array, a string, and a struct

```c
// suppose we want to allocate storage for n ints 
int *a;
a = malloc(n * sizeof(int)); // does not clear memory
a = calloc(n, sizeof*int));  // clears the memory

// suppose we want to allocate space to store a name called "david"
char *name;
name = malloc(strlen("david")+1);
strcpy(name, "david");

// suppose we want to allocate space for a struct instance
struct point {int x, y;} *p;
p = calloc(1, sizeof(struct point));
```

Note:

* Always use **`sizeof()`** to determine the unit space needed. Even if you know the size of int is typically 2 bytes, you don't know if every system treats it like so. 

## Deallocation 

The `free()` function: `void free(void *ptr);`frees the memory pointed by `ptr` which is previously allocated by `malloc()`, `calloc()`, and `realloc()`. 

Once the memory block is released, it can be reused subsequently, and the `ptr` remains as a pointer.

Note:

* Do not store anything new to that `ptr` because the `ptr` points to no memory. Be careful with this **dangling** pointer error.





