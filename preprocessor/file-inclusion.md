# File Inclusion

The file inclusion is achieved by `#include` directive. It has two forms, the first form is used for header files that belongs to C's own library, and the second form is used for all other header files including any that we write:

**FORM1 `#include <filename>`**

**FORM2 `#include "filename"`**

FORM1 searches the directories in which the system header file resides. On UNIX, they are kept in `/usr/include`. Don't put your file in FORM1, preprocessor won't find your file. 

FORM2 searches the current directory, then searches the directory in which system files reside. 

#### Absolute Path and Relative Path

An absolute path starts from a specific path or drive information, such information makes it difficult to compile when the program is transported to another machine or operating system.

While a relative path don't mention specific derives, and path are relative. 

Example of an absolute path and relative path:

```c
// absolute path
#include "\cprogs\include\utils.h"

// relative path 
#include "utils.h"
#include "..\include\utils.h"
```

#### Third FORM of an `#include` directive

**FORM3 `#include macro-name`** 

The third form takes in a macro-name, that has been defined with a token. Noticed that the macro-name must be defined and can be replaced by a file name. Shown by an example:

```c
#if defined(IA32)
    #define CPU_FILE "ia32.h"
#elif defined(IA64)
    #define CPU_FILE "ia64.h"
#elif defined(AMD64)
    #define CPU_FILE "amd64.h"
#endif

#include CPU_FILE
```



