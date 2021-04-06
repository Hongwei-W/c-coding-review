---
description: 'In this section: 1) if statements, and 2) switch statements.'
---

# Selection Statements

## `if` Statements 

* **FORM `if (expression) { ... }`**
* Non-zero values are "true"
  * Dangling else problem: without braces, an `else` belongs to the nearest `if` statement that hasn't paired with an `else` 
  * The following three code blocks are equivalent

    ```c
    // block 1
    if (y != 0)
        if (x != 0)
            result = x / y;
    else 
        printf("Error: y is equal to 0\n")
 
    // block 2       
    if (y != 0)
        if (x != 0)
            result = x / y;
        else 
            printf("Error: y is equal to 0\n")

    // block 3
    if (y != 0) {
        if (x != 0) {
            result = x / y;
        }
        else {
            printf("Error: y is equal to 0\n")
        }
    }
    ```

### Conditional Expressions \(Continue of Section 'Expression'\)

* **FORM `expr1 ? expr2 : expr3`**
* Read as: "if `expr1` then `expr2` else `expr 3`"
* Example \(the following two code blocks are equivalent\):

  ```c
  // block 1
  if (i > j) 
      printf("%d\n", i);
  else
      printf("%d\n", j);

  // block 2
  printf("%d\n", i > j ? i : j); 
  ```



## `switch` Statement 

* **FORM `switch (controlling-expr) {case case_label: expr; break;}`**
* Special cascaded `if` statement 
  * `if`: The `controlling-expr` is type `int/char`
  * `else if`: The `case_label` is a _constant_ only,  should not be a variable name, cannot also be a range; using `break` to finish this case, or it will fall into the next case block 
    * Constant: numbers that appear in the text of a program, not numbers that are read, written, or computed
  * `else`: `default` is acting like an else, collecting all remaining parts 
* Can put serval case labels on the same line
* Example \(the first two blocks \[`if` and `switch` statements\] are equivalent, the third block put serval case labels on the same line\):

  ```c
  // if
  if (grade == 4) {     
      printf("Excellent");
  } else if (grade == 3) {
      printf("Good");
  } else if (grade == 2) {
      printf("Average"); 
  } else if {grade == 1) {
      printf("Poor");
  } else if (grade == 0) {
      printf("Failing");
  } else {
      printf("Illegal grade");
  }

  // switch 
  switch (grade) {
      case 4: printf("Excellent");
              break;
      case 3: printf("Good");
              break;      
      case 2: printf("Average");
              break;
      case 1: printf("Poor");
              break;
      case 0: printf("Failing");
              break;
      default: printf("Illegal grade");
              break;

  // block 3
  switch (grade) {
      case 4: case 3: case 2: case 1: 
          printf("Passing");
          break;
      case 0:
          printf("Failing");
          break;
      default: 
          printf("Illegal grade");
          break;
  }
  ```

