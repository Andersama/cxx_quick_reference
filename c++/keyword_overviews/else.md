### Syntax
```c++
if (boolean-expression) compound-statment else if (boolean-expression) compound-statment else compound-statement
```
### Control Flow
An else block specifies a block of code to execute when a condition is false.
### Example
```c++
int i = 0;
if (false)
	i--;
else if (false)
	i-=2;
else
	i++; // i is now 1
```