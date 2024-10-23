### Syntax
```c++
assignable-expression or_eq expression
```
### Operator
Returns true or false, returns true if operands are all true.
### Example
```c++
bool left_handed = true;
bool right_handed = true;

bool handy = left_handed;
handy or_eq right_handed;
```