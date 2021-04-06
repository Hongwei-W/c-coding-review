# General Form of A C Program

## Typical directives

* Typical directives explained by an example

  ```c
  /* headers */
  #include <stdio.h>

  /* macros */
  #define FREEZING_PT 32.0f

  /* type definition */
  #typedef Degree int

  /* external variables */
  extern temp;

  /* global variables */
  int num_pt = 0;

  /* function declarations (prototypes) */
  void mst_prim(int n, int **point);

  /* main function */
  int main(void) {
      ...
  }

  /* function definition */
  void mst_prim(int n, int **point) {
      ...
  }
  ```





