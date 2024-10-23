### Syntax
```c++
struct identifier type-definition
```
### Type Definition
Defines a type, same as [[class]] but the default privacy of its elements are public.
### Syntax
```c++
template<typename T>
class dynamic_array {
	public:
	dynamic_array() = default;
	 // you can imagine that internally defining a class will put "public:" at the top of its definition
	private:
	T* ptr  = nullptr;
	int sz  = 0;
	int cap = 0;
}
```