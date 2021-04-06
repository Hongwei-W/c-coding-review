# Type Definitions

* **FORM `#typedef builtin-type New-type`**
* Define a data type using an existing data type 
* Then the newly-defined data type can be used the same as any built-in types to declare variables 
* Improving the code readability, easing modifying and portability 
* Example:

  ```c
  typedef float Dollars;
  Dollars cash_in, cash_out; // This is more informative 
  float cash_in, cash_out;   // Comparing to this 
  ```





