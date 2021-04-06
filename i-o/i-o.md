---
description: 'In this section: 1) formatting input/output'
---

# Formatting Input/Output

## Conversion Specifier

There are **conversion** **specifier** to indicates how to display in stdout, the general form `%-m.pX`:

* `-` is optional, indicating "left justification";
* `m` is optional, indicating "minimal field width";
* `p` is optional, indicating "number of digits after the decimal point", or "the first number of characters";
* `X` is required, indicating "types of printing":

  * `d` , `u` are base 10 signed and unsigned integer \(4 bytes, 32 bits\);
  * `hd`, `hu` are short signed, and unsigned integer \(2 bytes, 16 bits\);
  * `hhd`, `hhu` are short short signed, and unsigned integer  \(1 btye, 8 bits\);
  * `ld`, `lu` are long signed, and unsigned integer \(4 bytes, 32 bits OR 8 bytes, 64 bits\);
  * `lld`, `llu` are long long signed, and unsigned integer \(8 bytes, 64 bits\);
  * `o` is base 8 integer;
  * `x` is base 16 integer;
  * `f` is float;
  * `e` is float in exponetial format;
  * `p` is pointer address;
  * `c` is a single character;
  * `s` is a string;

      If `#include <inttypes.h>`:

  * `PRIi8`, `PRIu8` are int8\_t, and uint8_\__t integer;
  * `PRIi32`, `PRIu32` are int32\_t and uint32\_t integer;
  * `PRIi16`, `PRIu16` are int16\_t, and uint16\_t integer;
  * `PRIi64`, `PRIu64` are int64\_t, and uint64\_t integer.

## Escape Sequences 

There are escape sequences beginning with `\`, such as:

* `\n` indicates a newline \(newline character\);
* `\t` indicates a horizontal tab;
* `\"` types a `"`;
* `\\` types a `\`;
* `%%` types a `%`.



