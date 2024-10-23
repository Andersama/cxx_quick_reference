### Syntax
```c++
co_await expression
```
### Control Flow Coroutine
Executes expression in a separate context, waits for the evaluation to return with a result (for the separate context to return control back to the current application). This is a way to implement asynchronous operations.
### Example
```c++
for (size_t i = 0; i < 100; i++) {
	co_await write_to_console(i);
}
```
