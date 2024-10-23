### Syntax
```c++
friend function-declaration
friend function-definition
friend type-specifier
```
### Privacy Declaration
Allows another type to make use of protected or private members. This can be useful for tightly integrating several types together allowing transformations that might be prevented by being made private or protected.
### Example
```c++
class b_class {
	int a_special_internal_value;
	friend class a_class; // now a_class can access internals of b_class
public:
	constexpr b_class() = default;
}

class a_class {
	friend b_class; // Now b_class can access the internals of a_class
}
```