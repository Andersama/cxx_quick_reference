### Syntax
```c++
assignable_expression andeq expression
```
### Operator
Returns the result of the bitwise operator `&` and stores the result in the left operand.
### Example
```c++
//shorthand for &= operator
int mask = 0x4;
int value = 0x6;
int value and_eq mask;
//value is now 0x4;
```