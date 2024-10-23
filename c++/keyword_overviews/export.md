### Syntax
```c++
export function-prototype
```
### Function Specifier
Functions which are exported are made available for linking by external programs.
### Example
```c++
export int add(int a, int b) {
	return a + b;
}
// external programs can now find add and use the resulting code in their own binaries
```