### Syntax
```c++
mutable(optional) type
mutable(optional) pointer-type mutable(optional)
```
### Storage Specifier
The mutable storage specifier marks the type as being writable. This is the default behavior for all types. This is used specifically to deal with cases where a constant type may still need to modify a member variable to function.
### Example
```c++
struct a_type {
	mutable int status = 0;
	int value;
	void update_status(int new_status) {
		status = new_status;
	}
};

const a_type example;
example.update_status(1); //
example.value = 1; // compiler error
```