### Syntax
```c++
constexpr expression
if constexpr (condition) compound-statement
```
### Storage Specifier
Tells the compiler that the following expression should be processed at compile time, if the expression isn't evaluable in a compile time context, this will result in a compiler error. Compile time evaluated conditions are useful for selecting different implementations of code given already known pre-conditions. 
### Example
```c++
constexpr int value = 5 + 6; // value will be 11

if constexpr (value < 10) {
	// content of this compound statement will be ignored entirely by the compiler because value was >= 11, this is useful for selecting different implementations of code given already known pre-conditions because code which would otherwise potentially emit a compiler error can be skipped over.
} else {
	// content of this compound statement will be processed as if the condition was passed, the conditional if will be omitted in the generated code
}
```