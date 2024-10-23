### Syntax
```c++
goto label
```
### Flow Control
`goto` statements allow code to jump to an entirely different area of code.
### Example
```c++
loop_start:
int i = 0;
std::cout << i << '\n';
if (i < 100)
	goto loop_start;
std::cout << "exit loop";
```