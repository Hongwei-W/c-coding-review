# Conditional Compilation

Conditional compilation can let you include or exclude a section of the program text.

## How to Achieve Conditional Compilation

### The `#if` and `#endif` Directives 

**FORM `#if constant-expr` ...code-block... `#endif`**

We'll illustruate by an example:

```c
#define DEBUG 1

#if DEBUG
printf("value of i: %d\n", i);
printf("value of j: %d\n", j);
#endif 
```

We find that the two `printf()` is enclosed by an `#if` and `#endif`, we see that the evaluation of `if` depends on `DEBUG`. This is very intuitive, if we define such a macro called `DUBUG` and set its value to be a true value, then the two `printf()` are able to execute. Oppositely, if there is no such `DEBUG` has been defined, or defined to be a false value, then these two `printf()` are ignored. 

But if we enclose our code with **`if !constant-expr`**, reversely, the code block inside will execute if there is no such macro defined, or the macro is defined as a false value. 

```c
#if !DEBUG
printf("value of i: %d\n", i);
printf("value of j: %d\n", j);
#endif 

// two printf() will execute 
```

### The `defined` Operator

**FORM `#if defined(macro-name)` ...code-block... `#endif`**

This acts quite the same as the above one. However, `defined` is an operator just like the `#` and `##`. Other than that, `defined` operator only test for if the `macro-name` exist. So, the constant value of the macro does not need to be defined. Consider the following example:

```c
#define DEBUG

#if defined DEBUG // or if defined(DEBUG), they are the same
printf("value of i: %d\n", i);
printf("value of j: %d\n", j);
#endif 

// two printf() will execute
```

### The `#ifdef` and `#ifndef` Directives 

**FORM `#ifdef macro-name` ...code-block... `#endif`**

**FORM `#ifndef macro-name` ...code-block... `#endif`** 

These acts the same as the above `defined` operator.  That they all test for the existence of a macro. However, the code block enclosed by `#ifndef` evaluates only if the macro hasn't been defined.

### The `#elif` and `#else` Directives   

**FORM `#if constant-expr` ...code-block\(cb\)... `#elif constant-expr` ...cb... `#else` ...cb... `#endif`**

These are acted the same as the `if`, `else if`, and `else` in a program. However, it depends on the definition of a macro. 

The use of directives are in the middle of a normal program/code, so it will be a mess when nesting or defining a number of `#elif`. So, it is a good habit to comment what are these directives doing. For example:

```c
#if DEBUG
...
#endif /* DEBUG */
```

## Use of Conditional Compilation 

Clearly, the conditional compilation is useful for debugging, as it could include or exclude a block of code such as printing logs, but there are other uses. We just show some snippets instead of explaining thier full functionalities.

### Writing Programs That are Portable to Several Machines or Operating System

```c
#if defined(WIN32)
...
#elif defined(MAC_OS)
...
#elif defined(LINUX)
...
#endif
```

### Writing Programs That can be Compiled with Different Compilers 

```c
#if __STDC__
functiion prototyeps 
#else
old-style function declaration
#endif
```

### Providing a Default Macro Definition 

```c
#ifndef BUFFER_SIZE
#define BUFFER_SIZE 256
#endif
```

### Temporarily Disabling Code That Contains Comments 

```c
#if 0
lines containing comments 
#endif
```



\*\*\*\*







