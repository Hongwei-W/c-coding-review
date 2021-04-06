# Pointers To Pointers/Functions

## Pointers to Pointers

Pointers to pointers are useful in the following scenario. When an argument to a function is a pointer variable, we want the function to be able to **modify the variable by making it point somewhere else**. 

Explained by an example, in a linked list, we want the "adding a new node to the first position in the linked list" function to return nothing instead of a node pointer:

```c
// want to change the return value to void
struct node *add_to_list(struct node *head, int n) {
    struct node *new_node = malloc(sizeof(struct node));
    if (new_node == NULL) {
        exit(EXIT_FAILURE);
    }
    new_node->value = n;
    new_node->next = head;
    return new_node;
}
```

A straightforward thought would be to assign the head of the linked list, `head`, as `new_node`, which looks like `head = new_node;` in C code. However, this is **impossible** because a pointer is a **passed by value**, so the change of `head` is only effective in the function.



To make it possible, we correct the function in this way:

```c
void add_to_list(struct node **head, int n) {
    struct node *new_node = malloc(sizeof(struct node));
    if (new_node == NULL) {
        exit(EXIT_FAILURE);
    }
    new_node->value = n;
    new_node->next = *head;
    *head = new_node;
}
```

And we call the function by:

```c
add_to_list(&first, 10);
```

Explain: when calling the function, the address of `first` is provided. So, we can use `*head` as an alias for `first`. And assigning`new_node` to `*head` will modify `first`.  



## Pointers to Functions

### Parameters In A Function Definition 

Pointers to functions are useful when we need to call different functions with the same input, or performing different operations on the same data. 

In this case, a pointer to a function is used as an argument in another function, explained by an example of sorting programs with multiple sorting algorithms:

```c
// suppose we defined sorting functions 
void insertionsort(int *array, int left, int right);
void bubblesort(int *array, int left, int right);
void mergesort(int *array, int left, int right);
void quicksort(int *array, int left, int right);

// we set up a function that has a function pointer
// the function pointer given by the function call decide which sorting method 
//   will be used
void sort(void (*pf)(int *, int, int), int *array, int i, int j) {
    pf(array, i, j);
    return;
}

// suppose we want to use insertionsort 
sort(insertionsort, array, 0, n-1);
```

Explain:

* The function name \(`insertionsort`\) is supplied as the first argument. There are no parentheses after `insertionsort`. As the C compiler produces a pointer to the function and passes it to `sort()`.
* We can then call the function `insertionsort()` inside `sort()` as 

  ```c
  (*insertionsort)(array, i, j); // which equivenlents to 
  insertionsrot(array, i, j); 
  ```

* `*pf` represents the function that `pf` points to, each `(*pf)(array, i, j)` points to the actual function of `insertionsort(array, i, j)`. C allows writing `pf(array, i, j)` to call the function. As it seems more intuitive, it is more used. 

### Variable Store A Pointer To A Function

Explained by an example:

```c
// suppose we define a variable that can store a pointer to a function
void (*pf)(int);

// f is a function with an int parameter and a return type of void
// this is the same as how the pointer variable is defined 
pf = f;

// call f by writing
(*pf)(i);
// or 
pf(i);
```

### An Array of Function Pointers

Including a number of function pointers in an array would mimic the effect of a menu. The functions in the array are easily accessed by present the indices of the array. While a similar effect can be obtained using a switch statement, the elements of the \(functions in the\) array can be changed as the program is running.  

Explained by an example:

```c
void (*file_cmd[])(void) = {new_cmd, open_cmd, close_cmd, save_cmd};

// we can then subscript the file_cmd array and call the corresponding function
// supoose we want to call new_cmd()
(*file_cmd[0])(); 
//or
file_cmd[0]();
```

