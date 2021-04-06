# Macro Definition

The `#define` directive defines a **macro**, a name that represents something else, such as a constant or frequently used expression. 

The preprocessor runs multiple times until all the macro is replaced by the defined values, so the order of directives is not important. 

## Simple Macros

**FORM`#define indentifier (replacement-list)`**

Putting extra symbols such as `;` or `=` will cause the replacement to include those meaningless symbols. 

Wrong examples and a correct example are shown below:

```c
#define L 100
int a[L]; // correct example

#define N = 100
int a[N]; // incorrect, becomes int a[= 100];

#define M 100;
int a[M]; // incorrect, becomes int a[100;];
```

#### Controlling Conditional Compilation 

`#define DEBUG` for debugging. Yes, the replacement list can be empty

## Parameterized Macros

**FORM `#define identifier(x1, x2, etc.) (replacement-list)`**

The parameterized macros **serve as simple functions**. 

The parameters and `replacement-list` are enclosed by parentheses. The **parentheses are deterministic** and are suggested to be added for all variables, which avoids possible evaluation precedence error. Normally there are **no unnecessary spaces.** 

There is **no data type** for the parameters, so the parameters are generic. And the arguments aren't type-checked by the compiler.

Examples of parameterized macros:

```c
// nested parameterized macros
#define PI(i) (3.1415926*(i))
#define TWO_PI 2*PI(1)

// a user-defined GETCHAR() function
// notice that the parameters can be empty
#define GETCHAR() getc(stdin)
```

### Possible Mistakes

Macro definitions are intuitive, but meanwhile prone to produce mistakes. Sadly, these errors are so easy to omit because they are not part of the code,  that they could be hard to find and hard to debug.  

#### Side effect

You should always **avoid defining macros and using arguments with side effects.**

Explained by an example:

```c
#define MAX(x, y) ((x)>(y)?(x):(y))
// In the program
n = MAX(i++, j);
// will become
n = ((i++) > (j) ? (i++) : (j)); // notice the side effect if i > j
```

When `i` is greater than `j`, we want to advance `i`. However, in the code, the `i` gets advanced twice. 

If we replace `i` with a recursive function, things will get way worse:

```c
n = MAX(recur_func(++array_ptr, --size), array_ptr[0])
// this recur_func find the max number in an array
```

The side effect will cause the `array_ptr` to advance way many positions than we expected, and segmentation fault may occur.

#### Missing Parentheses

Without the parentheses, we cannot guarantee that the compiler will treat replacement lists and arguments as a whole expression. 

An example of a mistake caused by missing parentheses:

```c
// mistakes casued by losing parentheses
#define IS_EVEN(n) n%2==0
int i = 9, j = 1;
IS_EVEN(j + i); 
```

It is well-known that `j + i = 9` is an even number and should return us a `true`, but the program will return us a `false`. The reason why is that the replaced version given by the preprocessor is:

```text
j + i % 2 == 0
```

 The `i % 2` will be first evaluated as a `1`, then add `j` to be a `2` This is an example that is not equal to `0`. 

### Operators In Macro Definition

There are only two operators that are executed during preprocessing: 

* Stringization by `#`;
* Token Pasting by `##`.

#### Stringization

The `#` coverts a macro argument into a string literal, it can appear only in the replacement list of a parameterized macro.

Explained by an example:

```c
// to print not only the result of an expression, but also the expression itself
                         // ↓ creating a string based on argument
#define PRINT_INT(n) printf(#n " = %d\n", n) 

PRINT_INT(i/j);
// will becomes 
printf("i/j" " = %d\n", i/j);

// suppose 
int i = 11, j = 2;
PRINT_INT(i/j);
// in stdout
i/j = 5
```

#### Token Pasting

The `##` paste two tokens together to form a single token. 

If one of the operands is a macro parameter, pasting occurs **after** the parameter has been replaced by the corresponding argument.

Explained by an example:

```c
#define MK_ID(n) i##n
int MK_ID(1), MK_ID(2), MK_ID(3);
// after preprocessing, this will become
int i1, i2, i3; //three variables are created 
```

### Empty Macro Arguments \(In C99\)

C99 allows any or all of the arguments in a macro call to be empty. When calling, you should write the same number of commas to indicate position. But the argument can simple disappear from the argument list, and disappear from the replacement list \(function\). 

Examples of empty macro arguments:

```c
// we first define some macros
#define ADD(x, y) (x+y)
#define MK_STR(X) #x
#define JOIN(x, y, z) x##y##z

// then we call these macros 
int i = ADD(, k);
char empty_string[] = MK_STR();
int JOIN(a, b, c), JOIN(a, b, ), JOIN(a,, c), JOIN(,, c); // make variable names

// they are expanded into 
int i = (+k);
char empty_string[] = "";
int abc, ab, ac, c;
```

Explain:

* If an empty argument is "stringized" by the `#` operator, the result is `""` \(the empty string\);
* If one of the arguments of the `##` is empty, the arguments are first replaced by an invisible _placemaker_, after the compilation finished, the _placemaker_ then disappear from the program. 

### Creating Longer Parameterized Macros 

Some longer macros involve two or more expressions and statements. And some macro calls are embedded in an `if`, or loop, etc. These marcos are commonly defined with **`do {...} while(0)`** format. An example will be shown before explaining why we use it.

Suppose we define a macro that reads in from `stdin` and print in the `stdout`:

```c
#define ECHO(s)        \
        do {           \
          gets(s);     \
          puts(s);     \
        } while(0)      // Note, there is no semicolon after while(0)
```

And suppose we want to use it in the code where the execution of `ECHO` depends on a bool `echo_flag`, then the code:

```c
if (echo_flag)
    ECHO(str);
else
    gets(str);
    
// it will expand to 

if (echo_flag)
    do {
        gets(str);
        puts(str); 
    } while(0);
else
    gets(str);
```

You will find that the code runs as expected. See the missing `;` after `while(0)` in the macro definition is magically filled by the `;` after the macro call `ECHO(str)`? 

However, you might think of other solutions of defining macors, 1\) using a colon operator, or 2\) purely writing two expressions in a pair of braces. We will prove that the first one works but the second one cannot. 

If we use a colon operator:

```c
#define ECHO(s) (get(s), puts(s))

// this will expand to 

if (echo_flag)
    (get(s), puts(s));
else
    gets(str);
```

Thanks to the colon operator who evaluates both operands \(and discards the return value of the first operand\), we can have the expected outcome. But not all the macro definitions are as simple as this.

If we write two expressions in a pair of braces:

```c
#define ECHO(s) {get(s); puts(s)}

// this will expand to 

if (echo_flag)
    {get(s); puts(s)};
else
    gets(str);
```

This will **not** work. Notice the right brace and its following semicolon \(`};`\)? This is a sign of a `null` statement! It means that there is no `else` clause after `if`. So, the `else` clause will be totally ignored. But in `do{...} while (0)`example, the `;` after macros call fills the vacancy. 

Thus, by coding convention, we use **`#define identifier(arguments) do {...} while(0)` to write a long macro definition.** 

### Macros with a Variable Number of Arguments 

We define such a macro to pass these arguments to a function that accepts a variable number of arguments, such as `printf` and `scanf`. We'll illustrate the idea by an example:

```c
#define TEST(condition, ...) ((condition)?        \
    printf("Passed test: %s\n", #condition):      \
    printf(__VA_ARGS__))

// let's use TEST
TEST(voltage <= max_voltage, "Voltage %d exceeds %d\n", voltage, max_voltage);

// it will expand to 
((voltage <= max_voltage)?
  printf("Passed test: %s\n", "voltage <= max_voltage");
  printf("Voltage %d exceeds %d\n", voltage, max_voltage));
 
// if voltage <= max_voltage, then in stdout:
passed test: voltage <= max_voltage

// if voltage(125) > max_voltage(120), then in stdout:
Voltage 125 exceeds 120
```

Explain:

* We first notice the `...` inside the parameter list, it is known as _**ellipsis**_, goes at the end of a macro's parameter list and preceded by ordinary parameters if there is any;
* `__VA_ARGS__i` is a special identifier that can appear only in the replacement list of a macro with a variable number, it represents all the arguments that correspond to the ellipsis;

## An Inclusive Example -- MAX 

Notice how the previous `MAX` macro definition example acting unexpectedly due to the side effect. It seems that the only way to avoid the side effect is by defining an actual function. But as the function need a specific type, we need to define many similar `max` functions for each of them \(`int`, `float`, etc.\). But here, we provide another way, using macro definition, to not repeat yourselves. 

```c
#define GENERIC_MAX(type)          \
type type##_max(type x, type y) {  \
    return x > y ? x : y;          \
}
```

Suppose we need a `max` function that works with `float`, we can use code in block 1 to initialize, and the preprocessor will expand the code into block 2. To use the function, we simply call \(in block3\) it as we used to do. 

```c
// block 1
GENERIC_MAX(float)

// block 2
float float_max(float x, float y) {
    return x > y ? x : y;
}

// block 3
float_max(3.0, 4.0);
```

## Undefine And Redefine

**FORM `#undef identifier`** 

A macro **may not** be defined twice unless the new definition is identical to the old one. So, to define a macro with the same identifier with a different replacement list, use `#undef` first.

## Predefined Macros \(In C99\)

C has several predefined macros. Each macro represents an integer constant or string literal. These macros provide information about the current compilation or about the compiler itself. 

* `__LINE__` Line number of file being compiled \(to help locate errors\);
* `__FILE__` Name of file being compiled \(to help locate errors\);
* `__DATE__` Date of compilation \(in the form `Mmm dd yyyy`\);
* `__TIME__` Time of compilation \(in the form `hh:mm:ss`\);
* `__STDC__` `1` if the compiler conforms to the C standard C89 or C99;

  Less frequently used macros:

* `__STDC__HOSTED__`           `1` if this is a hosted implementation, `0` if it is freestanding;
* `__STDC__VERSION__`         The version of C standard supported;
* `__STDC_IEC_559__`           `1` if IEC 60559 floating-point arithmetic is supported;
* `__STDC_IEC_559_COMPLEX__`  `1`if IEC 60559 complex arithmetic is supported 
* `__STDC_ISO_10646__`        `yyyymmL` if `wchar_t` values match the ISO 10646 standard of the specified year and month 

An example of using `__DATE__`, `__TIME__` to indicate on which day this chapter has finished: 

```c
printf("This chapter was finished on %s at %s", __DATE__, __TIME__);
// In stdout, the following line will be printed
This chapter was finished on Apr 2 2021 at 10:43:08
```

Another example of using `__LINE__`, `__FILE__` to find out the division of 0 error:

```c
#define CHECK_ZERO(divisor)          \
    if (divisor == 0)                \
        printf("Attemp to divide by zero on line %d " \
        "of file %s", __LINE__, __FILE__)
// The CHECK_ZERO macro can be invoked prior to a divison 
CHECK_ZERO(j);
k = i / j; // assuming i and j are numbers 
// If j is a 0, then the following line will be printed 
Attemp to divide by zero on line 9 of file foo.c
```

## The `__func__` Identifier

The `__func__` has nothing to do with the preprocessor, but it is useful for debugging. Notice that the identifier is written in a lower case letter.

Every function has access to the `__func__` identifier. It behaves likes a string variable storing the name of the currently executing function. So, we are able to write these debugging macros:

```c
#define FUNCIION_CALLED() printf("%s called\n", __func__);
#define FUNCTION_RETURNS() printf("%s returns\n", __func__);
```

Above shows that `__func__` can be placed inside functions to trace their calls. Another use is that, it can be passed to a function to let it know the name of the function that called it. 

## Example in Project `nanomq`

There are many examples of macro definition in project `nanomq`, here, we take one simple `debug` macro and analysis it. And we paste some other uses for your  reference:

```c
// simple debug macro

#define debug(M, ...) fprintf(stderr, "[DEBUG] %s:%d: " M "\n",\
		__FILE__, __LINE__, ##__VA_ARGS__)
```

In this macro definition, we have variable number arguments/parameters. The first ordinary parameter, namely `M`, is the message given by the programmer. What if we want the message to be formatted using the conversion specifier? The  `__VA_ARGS__` gives us the ability to add those variables. And the token pasting `##` will strip out the `,` if there are no other variables provided. See the example below:

```c
// we use
debug_msg("In conn_param: the pro num is %hhu", p->conn_param->pro_ver);
	
// it will expand to 
fprintf(stderr, "[DEBUG] %s:%d: " "In conn_param: the ver num is %hhu" "\n",\
		__FILE__, __LINE__, p->conn_param->pro_ver)
		
// in stderr
Fri Apr  2 15:03:07 2021 nano_pipe_start: In conn_param: the ver num is 4
```

Other examples:

```c
#ifdef NDEBUG
#define debug(M, ...)
#else
#define debug(M, ...) fprintf(stderr, "[DEBUG] %s:%d: " M "\n",\
		__FILE__, __LINE__, ##__VA_ARGS__)
#endif

#define clean_errno() (errno == 0 ? "None" : strerror(errno))

#define log_err(M, ...) fprintf(stderr,\
		"[ERROR] (%s:%d: errno: %s) " M "\n", __FILE__, __LINE__,\
		clean_errno(), ##__VA_ARGS__)

#define log_warn(M, ...) fprintf(stderr,\
		"[WARN] (%s:%d: errno: %s) " M "\n",\
		__FILE__, __LINE__, clean_errno(), ##__VA_ARGS__)

#ifdef NOLOG
#define log(M, ...)
#define log_info(M, ...)
#else
#define log_info(M, ...) fprintf(stderr, "[INFO] (%s:%d) =========>> " M "\n",\
		__FILE__, __LINE__, ##__VA_ARGS__)

#define log(M, ...) fprintf(stderr, "[INFO] %s (%lu:%s:%d) " M "\n",\
		nano_get_time(), pthread_self(), __FUNCTION__, __LINE__, ##__VA_ARGS__)
#endif

#define check(A, M, ...) if(!(A)) {\
	log_err(M, ##__VA_ARGS__); errno=0; goto error; }

#define sentinel(M, ...)  { log_err(M, ##__VA_ARGS__);\
	errno=0; goto error; }

#define check_mem(A) check((A), "Out of memory.")

#define check_debug(A, M, ...) if(!(A)) { debug(M, ##__VA_ARGS__);\
	errno=0; goto error; }

#endif
```

