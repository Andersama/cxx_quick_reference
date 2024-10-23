### Syntax
```c++
operator operator-symbol
```
### Keyword
Used to define operator functions.
### Example
```c++
struct comparable_type {
	int value;
	bool operator<(const comparable_type &other) {
		return value < other.value;
	}
}
```