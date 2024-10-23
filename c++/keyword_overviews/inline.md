### Syntax
```c++
inline function-prototype
```
### Function Specifier
`inline` hints to the compiler that you would like to execute the function directly where the call is made. This very likely will increase the size of the program. Making certain functions inline may be a performance optimization.
### Example
```c++
inline int add(int a, int b) {
	return a + b;
}
```