### Syntax
```c++
assignable_expression bitand expression
```
### Operator
Returns the result of the bitwise operator `&`.
### Example
```c++
//shorthand for & operator
int mask = 0x4;
int value = 0x6;
int value = value bitand mask;
//value is now 0x4;
