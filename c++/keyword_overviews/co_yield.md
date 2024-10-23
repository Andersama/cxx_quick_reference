### Syntax
```c++
co_yield expression
```
### Control Flow Coroutine
Executes expression and returns its value to another context, execution of the current coroutine can continue from this point on, This is a way to implement asynchronous operations, or implement generator functions.
### Example
```c++
void iterate_from_to(int from, int to) {
	int current = from;
	for (; current < to; current++) {
		co_yield current;
	}
	co_return current;
}
```
