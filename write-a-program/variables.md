# Variables

## Local Variables/Function Parameters

**WHERE: local variable: declared in the body of a function, function parameters: initializied with arguments, local to the function** 

**LIFE SPAN: automatic storage duration** \(ie. allocate when enclosing function is called, deallocate when the function returns\)

**VISIBILITY: block scope** \(ie. visible from its declaration to the end of enclosing body\)

## `static` Local Variables 

**WHERE: declared in the body of a function, local to the function**

**LIFE SPAN: permanent storage duration** \(ie. allocate when the program starts, deallocate when the program terminates\)

**VISIBILITY: block scope** 

Other notes: 

* When a `static int` variable initialize, it equal to 0
* For future calls of the same function/block, the variable carries its last-used values 

## External Variables 

**WHERE: declared outside the body of a function, global \(counterpart to local\)**

**LIFE SPAN: permanent storage duration** 

**VISIBILITY: file scope \(ie. visible from its declaration to the end of enclosing file\)**

Other notes:

* Normally, an external variable is accessed/modified by multiple functions





