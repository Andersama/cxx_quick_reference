### Syntax
```c++
enum identifier enum-definition
enum identifier : integral-type enum-definition
```
### Type Definition
Enums specify identifiers with set values, these are useful for remembering special constant values that are used often by giving them names.
### Example
```c++
enum error_type {
	none, // none = 0
	too_many, // too_many = 1
	too_few, // too_few = 2
	missing_value = 3
}
```
