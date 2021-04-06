# Strings

A string is a series/sequence of characters enclosing by double quotes `"`and ending by a null character `\0`, so it can be defined as a char-type array.

Note:

* `char` encloses by single quotes `'`
* \(If there are many `\0` in the string\), the first `\0` indicates the end of the string. So, a string contains at least one `\0` and all characters after that is discarded
* The `\0` occupies 1 byte, but not counted into the length of the string
* An empty string `""` is stored as a single null character `\0`

## Two Kinds of Strings 

### String Constants \(String Literals\)

**FORM `char *pointer-name = "str";`** 

A String literal is stored as an array and treated as a `char *` \(type `char` pointer\). The assignment above doesn't copy the characters, it merely makes the pointer point to the first character of the string. 

No character of a string literal can be modified, as its name suggested.

### String Variables 

**FORM `char variable-name[str-length+1] = "str";`**

The reason why needing `+1` length is to store the extra `\0` byte. 

Doesn't `+1` resulting have no `\0`, which can not be used as a string. However, the compiler won't give any warning or error. 

The `str-length+1` can be omitted. The compiler will automatically allocate the correct number of spaces for the string.

### Compare Two Types 

By an example:

```c
char *date     = "June 14"; // a string constant
char date[]    = "June 14"; // a string variable
```

* In the string variable version, the characters stored in `date` can be modified. In the string constant version, the character cannot be modified.
* In the string variable version, `date` is an array name. In the string constant version, `date` is a variable that can be made to point to other string during program execution.

If we just define: 

```c
char *date;
```

* The compiler set aside enough memory for a pointer variable, but doesn't allocate space for a string

But if we define:

```c
char str[STR_LEN+1], *date;
date = str;
```

* `date` now points to the first character of `str`, so `date` can be used as a string.

### Summary

by example:

```c
char date1[8]     = "March 8";     // a valid string variable, can be modified 
char date2[10]    = "March 8";     // a valid string variable, can be modified 
char date3[7]     = "March 8";     // an invalid string varibale 
char date4[]      = "March 8";     // a valid string variable, can be modified 
char *char5       = "March 8";     // a valid string constant, cannot be modified
char date6[]      = {'M', 'a', 'r', 'c', 'h', ' ', '8'}; 
                                   // an invalid string variable
```

Note \(one unexpected outcome using `date3`\):

* If `date3` is initialized and `printf("%s", date3);` is used, the printing function won't stop until it reaches the first `\0`.

## Accessing Characters In A String 

Characters can be accessed by array or pointer, explained by an example:

```c
char str[STR_LEN + 1];
char *s, *t = "March 8";
int i;
...
printf("%c%c%c", str[i], t[3], *t); // these three are all valid 
```

## Arrays of Strings 

### Using A 2-Dimensional Character Array

Explained by an example:

```c
char student[][24] = {"Rupehra", "Kevin Joseph", "Matthew"};
```

Notes:

* 3 rows, each row has 24 bytes \(`sizeof(char)`\), all the unused space will be `\0`
* Students' names can be changed

### Using An Array of Characters Pointers

Explained by an example:

```c
char *student[] = {"Rupehra", "Kevin Joseph", "Matthew"};
```

Notes:

* 3 rows, the row length depends on the length of the string, plus one byte for `\0`
* Students' names cannot be changed

## String Functions 

There are **no** operators for copying or comparing strings, but there are function in the header file `<string.h>`. The function parameters are `char-ptr`,  and the arguments can be array, pointers, or string literals. 

It is a good habits to use `const char *char-ptr` as arguments, because the content of an array may be changed by the function. 

### String Copy 

**FORM `char *strcpy(char *s1, const char *s2);` OR `char *strncpy(char *s1, const char *s2, size_t n);` RETURN `char *s1` \( s2 is copied into it\)**

Copying `s2` up to the first `\0`.

`strcpy()` won't check if the copy of the string uses up the space of `s1` or not, so it is better to use `strncpy()` if not sure about the length.

If the length of the string stored in `s2` is greater than or equal to the size of the `s1` array, it will leave the `s1` without a terminating `\0`. So, here is a safer way to use `strncpy()`:

```c
strncpy(s1, s2, sizeof(str1)-1);
str1[sizeof(str1)-1] = '\0';
```

### String Length

**FORM `size_t strlen(const char *s);` RETURN `size_t` \(length of the array\)**

Won't count the null character.

### String Concatenation 

**FORM `char *strcat(char *s1, const char *s2);` OR `char *strncat(char *s1, const char *s2, size_t n);` RETURN char\* s1 \(s2 append to the end of s1\)**

Appending `s2` to the end of `s1`, and the null character of `s1` is over-written.

`strcat()` won't check if the concated string uses up the space of `s1` or not, so introducing `strncat()` to limit the number of character copy. `strncat()` is slower than `strcat()`, a call of `strncat()` will be like:

```c
strncat(str1, str2, sizeof(str1)-strlen(str1)-1);
```

### String Comparison 

**FORM `int strcmp(const char *s1, const char *s2);` RETURN `size_t`**

Using dictionary order and ACSII character set, return a number greater than 0 if `s1` &lt; `s2`; a number greater than 0 if `s1` &gt; `s2`; a number equal to 0 if `s1 == s2`.

### **Writing Content Into A String**

**FORM `sprintf(char *str, format, max-length);` OR `snprintf(char *str1, size_t n, format, max-length);`** 

Automatically adding `\0` 

To limit the number of character printed, use `snprintf()`

\*\*\*\*

