### Syntax
```c++
co_return expression
```
### Control Flow Coroutine
Executes expression and returns its value to another context, finalizes the execution of the current coroutine, This is a way to implement asynchronous operations.
### Example
```c++
void write_to_console(int i) {
	std::cout << i << '\n';
	co_return i;
}
```
