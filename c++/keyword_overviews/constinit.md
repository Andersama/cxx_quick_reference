### Syntax
```c++
constinit expression
```
### Storage Specifier
Tells the compiler that the following expression should be processed and assigned at compile time, if the expression isn't evaluable in a compile time context, this will result in a compiler error. Also can be used to hint that an external variable must have already been initialized.
### Example
```c++
constinit int value = 5 + 6; // value will be 11

if constexpr (value < 10) {
	// content of this compound statement will be ignored entirely by the compiler because value was >= 11, this is useful for selecting different implementations of code given already known pre-conditions because code which would otherwise potentially emit a compiler error can be skipped over.
} else {
	// content of this compound statement will be processed as if the condition was passed, the conditional if will be omitted in the generated code
}

extern thread_local constinit int imported_variable;
int check_imported_variable() {
	return imported_variable; // constinit has hinted to the compiler that the imported_variable must have been initialized elsewhere and does not need to protect the access of this variable
}
```