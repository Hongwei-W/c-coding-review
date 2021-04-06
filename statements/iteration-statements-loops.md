---
description: >-
  In this section: 0) how a loop works, 1) while statement, 2) do statement, 3)
  for statement, 4) method of exiting from a loop (break, continue, goto)
---

# Iteration Statements \(Loops\)

## Loop Overview 

* Loop are statements to be repeatedly executed, these statements are called _loop body_
* Variables initialized inside the _loop body_ are not able to be accessed outside the loop \(not _visible_\)
* To let a loop start, there is a  `controlling-expr` that evaluates each time the loop body is executed
* There are three iteration statements, namely `while`, `do`, `for`

## `while` Statement

* **FORM `while (controlling-expr) {statements}`**
* If `controlling-expr` is `false`, the loop body won't execute
* Usually, when the loop terminates, the `controlling-expr` must be false

### Infinite `while` Loop

* **FORM `while (1) {statements}`**
* Use a _loop-exiting statement_ to terminate 

## `do` Statement

* **FORM `do { statements } while (controlling-expr);`**
* If `controlling-expr` is false in the first place, the loop body will execute one time before exiting the loop \(different from `while` statement\), so **the loop executes at least once**
* Usually, when the loop terminates, the `controlling-expr` must be false

## `for` Statement

* **FORM `for ( initialization; controlling-expr; finishing-expr ) {statements}`**
  * `initialization` 
    * Executes only when entering the `for` loop
    * Omitted if _counting variable_ is initialized prior
    * **The variables initialized in the `initialization` can be accessed only in the loop** 
  * `controlling-expr` 
    * Executes every iteration to determine if entering the loop body or not
    * Omitted if an infinite loop, that is, terminates by a _loop-exiting statement_
  * `finishing-expr` 
    * Executes at the end of the loop body
    * Omitted if no `finishing-expr` or that expression \(usually advance the counting variable\) is included in the loop body 
* `for` loops are ideal for a loop having  a **counting** variable 

### Infinite `for` Loop

* **FORM `for (;;) {statements}`**
* Use a _loop-exiting statement_ to terminate 

## Convert `for` And `while`

* Illustrates by the following coding block: 

  ```c
  // for loop
  for (initialization; controlling-expr; finishing-expr) {
      statements
  }

  // while loop
  initialization;
  while (controlling-expr) {
      statements
      finishing-expr
  }
  ```

* Advantage using `for`: having a `for` statement declares its own control variable makes programs easier to understand 
* Advantage using `while`: the _counting-variable_ can still be accessed outside the loop

## Exiting From A Loop

### `break` Statement

* Can also be used to jump out of a `switch` statement,  `while`, `do`, `for` statement, but only jump out of the **innermost loop**

### `continue` Statement

* Terminates the current iteration, transfers control to a point just _before_ the end of the loop body 
* Control remains inside the loop

### `goto` Statement

* **FORM** 

  ```c
  identifier: statement
  ...
  ...
  for (;;) {
      ...
      goto identifier;
      ...
  }
  ```

* Jumping to any statement in the same function
* Useful when want to jump out multiple loop/braced-blocks
* Example where `goto` work but `break` won't \(maybe a `return` can help\)

  ```c
  identifier: statement
  ...
  ...
  for (;;) {
      ...
      goto identifier;
      ...
  }
  ```







