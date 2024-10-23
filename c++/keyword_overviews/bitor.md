### Syntax
```c++
assignable_expression bitor expression
```
### Operator
Returns the result of the bitwise operator `|` and stores the result in the left operand.
### Example
```c++
//shorthand for | operator
int mask = 0x1;
int value = 0x6;
int value = value bitor mask;
//value is now 0x7;
