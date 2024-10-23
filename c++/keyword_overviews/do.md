### Syntax
```c++
do compound-statement while (boolean-expression);
```
### Control Flow
A do while loop represents a loop in which the boolean expression is tested after the loop has been entered at least once. This can be a performance optimization.
### Example
```c++
int i = 0;
do {
	std::cout << i << '\n';
	i++;
} while (i < 100);
```