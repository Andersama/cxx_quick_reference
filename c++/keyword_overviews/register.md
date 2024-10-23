### Syntax
```c++
register identifier
```
### Specifier
Marks a parameter of a function to be stored in a register, this is a keyword brought over from c for the same purpose, currently it only hints to the compiler that it should store the parameter in a register as this is the default behavior for `c++`'s calling convention.
### Example
```c++
int add(register int a, register int b) {
	return a + b; // because a and b are marked as registers in theory they won't have an address*
}
```