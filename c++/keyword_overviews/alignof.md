### Syntax
```c++
alignof(expression)
```
### Operator
Returns specifies the alignment for classes or structs.
### Example
```c++
struct alignas(8) a_type {};
a_type value;
alignof(a_type); //returns 8
alignof(value); //reutrns 8

struct b_type {
	int count;
	int loops;
};

alignof(b_type); //returns 4
```

