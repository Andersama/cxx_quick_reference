### Syntax
```c++
reinterpret_cast<type>(expression)
```
### Casting Operation
Treats the expression as the new type, this is conceptually a no-op. In essence instructs the compiler to treat expression as if it were type instead. Unlike other casts, this will not transform or modify the original expression. This is the most dangerous cast, as it allows unchecked pointer to pointer conversions.
### Example
```c++
int add_float_as_int(float a, int b) {
	int* ptr_a = reinterpret_cast<int*>(&a);
	return *ptr_a + b;
}
```