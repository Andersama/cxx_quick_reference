### Syntax
```c++
alignas(expression)
alignas(type-id)
alignas(pack...)
```
### Specifier
Overrides or manually specifies the alignment for classes or structs.
### Example
```c++
struct alignas(8) a_type {}; //alignment of a_type is now 8 as opposed to 1
```