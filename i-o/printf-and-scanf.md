---
description: 'In this section: 1) printf(), and 2) scanf()'
---

# Formatting Input/Output Functions

## `getchar()` and `putchar()`

### `getchar()`

**FORM `ch = getchar();`, RETURN `int` or `EOF`**

Read a single character 

**Idiom:**

* Skipping the rest of the line: `while (getchar() != '\n');`
* Skipping the blanks: `while (getchar() == ' ');` 

### `putchar()`

**FORM `putchar(ch);`, RETURN `int` or `EOF`**

Write a single character 

## `printf()` and `scanf()`

Need `#include <stdio.h>` header file 

### `printf()`

**FORM `printf(formatted_string, var1, var2, ...);`**

### `scanf()`

**FORM `scanf(formatted_string, &var1, &var2, ...);` , RETURN `int` \(\# of value read in\)**

The variables \(lvalues\) must have memory units to store the contents read by `scanf()`.

Store things in an address, `&` will precede each variable to obtain the address of that variable \(more will be discussed in Section Pointers\).

A more intuitive format: `scanf(formatted_string, memory_addr1, memory_addr2, ...);`.

The program should know the types to store, so also use conversion specifiers.

#### How `scanf()` Works

1. Locate an item of the appropriate type;
2. **Skips blank** **space** if necessary;
3. Stop at an inappropriate character; 
4. **Put this last character back to the buffer;**
5. Return the **number of values** successfully read in \(good practice: check return value\).

Notes: 

* `scanf()` peeks the `\n` \(newline character\) without reading it \(remains in the buffer\), so when next time call `scanf()`, the `\n` will be the first reading in

One example of how `scanf()` works:

```c
scanf("%d/%d", &var1, &var2);
// suppose a number is type as "_5_/_96" ("_"represents a white space)
// scanf() can only strip the white space in front of 5, but not the one after 5
// so that white space remains and will casue error
```

## `gets()` and `puts()`

### `gets()`

**FORM `gets(char-pointer);`**

`gets()` does not strip space in the front, does not stop at a blank space, but reads in an entire line \(stops at a new-line character\).

Note:

* The `char-pointer` given should be initialized as an array \(string variable\), not a type `char` pointer;
* The compiler does not check whether `char-pointer` is full;
* Thus, introducing `fgets()`.

### `puts()`

**FORM `puts(char-pointer);`**

`puts()` has no conversion specification, always applies `"\n"` after.



