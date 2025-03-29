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

class contact  {
	std::string name;
	std::string phone_number;
	std::string address;
public:
	std::string& get_name() {return name;}
	std::string& get_phone_number() {return phone_number;}
	std::string& get_address() {return address;}
}
```