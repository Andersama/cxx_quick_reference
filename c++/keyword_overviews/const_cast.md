### Syntax
```c++
const_cast<target_type>(expression)
```
### Cast Operator
Removes const from a const qualified type. Careful when using this, as you can remove the compiler's guarantees about const using this cast.
### Example
```c++
int value = 5;
const int* const_ptr = &value;
int* ptr = const_cast<int*>(const_ptr);
*ptr = 4; // Although this is no longer a compiler error, this opens the possibility of run-time errors if value was made read-only by placing it in read-only memory! const_cast tends to be useful when dealing with templates
```
