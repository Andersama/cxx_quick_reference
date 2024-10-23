### Syntax
```c++
class identifier type-definition
```
### Type Definition
Defines a type, same as [[struct]] but the default privacy of its elements are private.
### Syntax
```c++
template<typename T>
class dynamic_array {
	private: // you can imagine that internally defining a class will put "private:" at the top of its definition
	T* ptr  = nullptr;
	int sz  = 0;
	int cap = 0;
	public:
	dynamic_array() = default;
}
```