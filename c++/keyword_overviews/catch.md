### Syntax
```c++
catch (expression) compound-statement
```
### Control Flow
Defines a handler to process exceptions which are of a particular [[type]] defined by the expression.
### Example
```c++
try {
	// Any code here, if an exception gets thrown at any point in this compound-statement catch handlers will process the errors
} catch (...) { // ... will process any remaining unhandled exceptions
	
}
```