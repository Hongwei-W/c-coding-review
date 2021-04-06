# Command Line Arguments

The `main()` is defined to have exactly two parameters, `int main(int argc, char *argv[]);`.

The arguments are passed by command line instead of `stdin`.

Explained by an example:

```text
test@test: ~/Desktop>./prog -i
```

The effect is that `OS` creates an array of strings:

* `argc` = 2, because there are two elements \(executable `./prog` and `"-i"`\);
* `argv[0]` points to the executable name `./prog`;
* `argv[1]` points to the string `"-i"`;
* `argv[2]` points to a null string `\0`.

Setting the parameter as `void` to accepts no arguments, `int main(void);`.

## Iterating Through Command Line Arguments 

One way uses an integer variable as an index into the `argv` array:

```c
int i;
for(i = 1; i < argc; i++) {
    printf("%s\n", argv[i]);
```

Another way is setting up a pointer points to `argv[1]` and advancing it until encountering a `\0`:

```c
char **p;
for(p = &argv[1]; *p != NULL; p++) {
    printf("%s\n", *p);
```



