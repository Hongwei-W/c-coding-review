---
description: >-
  In this section: 1) the null statement, and 2) dummy continue statement and
  empty compound statement that acted the same as null statement
---

# The null Statement

## The `null` Statement

* As the name suggested, does nothing 
* One of the examples is infinite `for` loop \(`for (;;)`\) that has a `null` initialization, however this is a `null` expression, not statement

### Primarily Use For Loop With Empty Body

* Another example \(the two blocks of code are equivalent\)

  ```c
  // normal version
  for (d = 2; d < n; d++) {
      if (n % d == 0)
          break;
  }
  if (d < n) 
      printf("%d is disvisible by %d\n", n, d);
    
  // simplified verison (with the null statement)
  for (d = 2; d < n && n % d!= 0; d++); // empty loop body 
  if (d < n) 
      printf("%d is disvisible by %d\n", n, d);
  ```

* Note: accidentally put a `;` after the parentheses in an `if`, `while`, or `for` statement creates a `null` statement, thus ending the `if`, `while`, `or` for prematurely
* However, the empty loop body with `null` statement is not standing out, to make it more visible can use 1\) a **dummy `continue` statement** or 2\) an **empty compound statement**

## The Dummy `continue` Statement

* The following example is the same as the block of code above \(the simplified version\)

  ```c
  for (d = 2; d < n && n % d!= 0; d++)
      continue;
  ```

## The Empty Compound Statement

* The following example is the same as the block of code above \(the simplified version with the  `null` statement\)

  ```c
  for (d = 2; d < n && n % d!= 0; d++)
      {}
  ```

