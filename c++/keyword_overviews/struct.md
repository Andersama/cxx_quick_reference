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

struct contact {
	std::string name;
	std::string phone_number;
	std::string address;
/* The getter functions as per the class example would be only
be necessary if the members were private
public:
	std::string& get_name() {return name;}
	std::string& get_phone_number() {return phone_number;}
	std::string& get_address() {return address;}
	*/*
}
```