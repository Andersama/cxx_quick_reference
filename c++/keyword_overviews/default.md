### Syntax
```c++
default: compound-statement
function-prototype = default
```
### Control Flow
In a control flow context default defines a failover case when no other case matches.
### Function Definition
When defining a member function of a struct, default can be used in a number of cases to use compiler generated function definitions as a shorthand, this includes constructors and as of C++23 comparison operators.
### Example
```c++
int value = 2;
switch(value) {
case 0:
case 1:
default:
	break;
}

struct a_type {
	int value = 0;
	a_type() = default; // use compiler generated contructor
}
```
