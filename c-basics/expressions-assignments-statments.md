---
description: >-
  In this section: 1) expressions (arithmetic, relational, equality, logical,
  comma) and their operators, 2) assignments, and 3) the precedence of
  evaluation
---

# Expressions, Assignments

## Expressions 

### Arithmetic Expressions \(Operators\)

#### Unary \(one operand, right asoociative\): `+`, `-`

* example: `i = +1`

#### Binary \(two operands, left asoociative\): `+`, `-`, `*`, `/`, `%`

* example: `1/10`, `1.0/10`
* Note
  * No zero divisor
  * `/`, `%` produce truncated \(floor\) result when two operands are integers
  * Meanwhile, `%` accepts only integer operand

#### In-/de-crement operators \(prefix: one operand, left associative; postfix: one operand, right associative\): `++`, `--`

* example: `i++`
* Note:
  * The side effect may modify the values of the operand 
  * example: `int i = 1; printf("i is %d, ++1); // stdout: i is 2` 

    `int i = 1; printf("i is %d, i++); // stdout: i is 1`

### Relational Expressions \(Operators\)

#### Relational Operators \(two operands, left associative\): `<`, `>`, `<=`, `>=`

* A relational expression yields either 0 or 1
* example: `1 < 5` yields `1`, while `1 < 2.5 < 1.1` yields `1`

### Equality Expressions \(Operators\)

#### Equality Operators \(two operands, left associative\): `==` , `!=`

* An equality expression yields either 0 or 1
* example: `(i >= j) + (i == j)` is either `0`, `1`, `2`

### **Logical Expressions \(Operators\)**

#### Logical Operators \(unary operands, left associative\): `!`; \(two operands, left associative\):  `&&`, `||`

* A logical expression yields either 0 or 1
* Note: **short circuit evaluation \(lazy evaluation\)** 
  * and: evaluates from left to right until the first "false" value - true only if both operands are true
  * or: evaluates from left to right until the first "truth" value - true if ate least one operand is true 
* example: `(i != 0) && (i==j)`

### Comma Expressions \(Operators\)

#### Comma Operators \(two operands, left associative\): `,` 

* **FORM `expr1, expr2`**
  * `expr1` is evaluated, and its value is discarded
  * `expr2` is evaluated, and its value is the value of the entire expression `expr1, expr2`
  *  Evaluating `expr1` should have a side effect, shown by the following example

    ```c
    int i = 1;
    int j = 5; 

    int k = ++i, i+j // k is 2 + 5 = 7
    ```

### Conditional Expression \(Operators\)

#### Conditional Operators \(three operands\): `... ? ... : ...`

* Will be covered in STATEMENTS -&gt; Selection Statements

## Assignments

### Assignment Operator \(two operands, right associative\): `=`

* Type conversion applies when operands have different types 
  * example: `int x = 7.2;`
* Right associativity and side effect 
  * example: `i = j = k =72;`
  * example: `int i; float f; f = i = 33.3f; // i is 33 but f is 33.0`
* The left operand should be an lvalue and is an object stored in memory 
  * wrong-example: `72.99 = i;`

### Compound Assignment 

* The compound assignment operator is composed of an assignment operator `=` and an arithmetic operator \(listed above\) 
  * example: `i = i + 2`

### Simplified Compound Assignment Operators \(two operands, right associative\): `+=`, `-=`, `*=`, `/=`, `%=`

* If using the old value to compute its new value, these operators can be simplified 
* example: the above example can be simplified as `i += 2`
* Note: 
  * If reverse the assignment and arithmetic operator, it merely copies the right operand to the left 
  * example: `i = (+j) // Merely copies the value of j into i`

## The Precedence of Operating 

From first to last 

* Postfix `++`, `--`
* Unary `+`, `-` and Prefix `++`, `--` and Unary `!`
* Binary `*`, `/`, `%`
* Binary `+`, `-`
* Binary `<`, `>`, `<=`, `>=`
* Binary `==`, `!=`
* Binary `&&`, `||`
* Assignments `=`, `+=`, `-=`, `*=`, `/=`, `%=` 



