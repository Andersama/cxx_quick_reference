### Syntax
```c++
decltype(expression)
```
### Type Specifier
Determines the type of an expression, useful when dealing with templates.
### Example
```c++
template<typename T>
auto output(const T& value) {
	std::cout << value << '\n';
}

template<typename T>
auto output_value(const T& value) {
	decltype(typename std::remove_cvref<T>::type) tmp = value;
	return std::thread([tmp](){
		output(tmp)
	});
}
```
