### Syntax
```c++
namespace declarations
```
### Scope
A namespace helps organize code, this is useful for writing code without accidentally creating naming conflicts with other code.
### Example
```c++
namespace std { // This is the standard library's namespace adding code to it may result in undefined behavior
}
namespace mynamespace {
	struct mytype {
		
	}; // We can make use of this type via the scope operator
	// mynamespace::mytype
}
```