### Syntax
```c++
consteval function-definition
```
### Storage Specifier
Tells the compiler that the following expression should be processed at compile time and that the following result must be compile-time evaluable as well, if the expression or result isn't evaluable in a compile time context, this will result in a compiler error.
### Example
```c++
consteval int square(int n) {
	return n*n;
}
constexpr int squared = square(5);
int nonconst_squared = square(5); // compiler error
```