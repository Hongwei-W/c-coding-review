# \#error, \#line, and \#pragma

## The `#error` Directive

**FORM `#error message`**

Encountering a `#error` means that there is a serious flaw in the program. Some compilers will immediately terminate compilation without finding out where the error is. 

With this being said, a `#error` is frequently defined in a `#else` clause. There are two examples, one is checking if the system supported `INT_MAX` is at least 100,000, another is checking if the code could be compiled under the current operating system.

```c
// check if the INT_MAX (largest possible int macro) is ate least 100,000
#if INT_MAX < 100000
#error int type is too small 
#endif 

// if INT_MAX < 100000, in stdout
Error directive: int type is too small

// check if the code can be compiled under the operating system
#if defined(WIN32)
...
#elif defined(MAC_OS)
...
#elif defined(LINUX)
...
#else
#error No operating system specified 
#endif

// if no operating system has benn specified as one of the three
Error, directive: No operating system specified 
```

## The `#line` Directive 

There are two forms of the \#line directive, both of them are altering how way program lines are numbered. As the use of `#line` is less frequent, here we only show the two forms without providing a further explaination.  

**FORM1 `#line n`**

This form after the line number by n, n+1, n+2, and so on

**FORM2 `#line n "file"`**

The lines that follow this directive are assumed to come from a _file_, with line numbers starting at _n._

## The `#pragma` Directive and `_Pragma` Operator

### The `#pragma` Directive

The `#pragma` directive provides a way to request special behaviour from the compiler. 

**FORM `#pragma tokens`**

`#pragma` directives can be very simple, or can be much more elaborate, here we show an example:

```c
#pragma data(heap_size >= 1000, stack_size => 2000)
```

The set of commands that can appear in `#pragma` is different for each compiler, so consult documentation first to see which commands it allows and what those commands do. The preprocessor must ignore any `#pragma` directive that contains an unrecognized command, it's not permitted to give an error message. 

There are three standard pragmas, all of which use `STDC` as the first token following `#pragma`. These pragmas are `FP_CONTRACT`, `CX_LIMITED_RANGE`, and `FENV_ACCESS`.

### The \_Pragma Operator 

The `_Pragma` operator is used in conjunction with the `#pragma` directive, it solves the limitation of the preoprocessor. The fact that a preprocessing directive cannot generate another directive \(while an operator can appear multiple times\).

**FORM `_Pragma (string-literal)`**

The `_Pragma` operator destringize its `string-literal`. It removes the double quotes and replaces the escape sequences with normal characters. In short, `_Pragma` turns its `string-literal` into another `#pragma token`. We see an example:

```c
#define DO_PRAGMA(x) _Pragma(#x)  // The `#` stringlized the x
// macro is used as               // _Pragma destringlized its string-literal
DO_PRAGMA(GCC dependency "parse.y") 
// will be expanded to 
#pragma GCC dependency "parse.y"
```

### Example in Project nanomq

Project nanomq used `#pragma` a couple of times, here are the examples and their corresponding explanations give by [gcc.gnu.org](https://gcc.gnu.org/onlinedocs/gcc/Diagnostic-Pragmas.html):

```c
#pragma GCC diagnostic push
#pragma GCC diagnostic ignored "-Wunused-result"
	(void) write(wfd, &c, 1);
#pragma GCC diagnostic pop
```

Explain:

* `#pragma GCC diagnostic push/pop` causes GCC to remember the state of the diagnostics as of each `push`, and restore to that point at each `pop`. If a `pop` has no matching `push`, the command-line options are restored;
* `#pragma GCC diagnostic ignore "-Wunused-result"` causes GCC to ignore the warning of all unsued result.

