### Syntax
```c++
static_cast<type>(expression)
```
### Casting Operation
Attempts to convert the expression using implicit and user defined functions to suit the new type. This operation is fully type checked, if no conversion operation is found, this will result in a compiler error. 
### Example
```c++
int add_float_as_int(float a, int b) {
	int* ptr_a = static_cast<int*>(&a); // Error: Invalid type conversion!
	int val_a = static_cast<int>(a); // Ok, performs a downcast from a float to an int.
	return *ptr_a + b;
}
```