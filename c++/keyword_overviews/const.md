### Syntax
```c++
const(optional) type
const(optional) pointer-type const(optional)
```
### Storage Specifier
The const storage specifier marks the type as being some form of read-only. The compiler is responsible for restricting usage of variables in such a way that the value will not change for its lifetime.
### Example
```c++
int value = 5;
value = 4;

const int const_value = 5;
const_value = 4; // compiler error, you can't modifiy a constant!

//defines a pointer to a constant value, note the pointer itself may be modified!
const int *ptr = &const_value;
ptr += 1; // ok, we're not modifiying the "constant" values that the pointer would lead us to
*ptr = 3; // compiler error

int * const a_constant_pointer = &value;
a_constant_pointer += 1; // compiler error, here we told the compiler that the pointer itself was constant, but it points to an int, which means we could modify it if we wanted
*a_constant_ptr = 3; // this is ok

const int * const a_truly_constant_pointer = &value;
// as you can imagine, trying to modify eaither the pointer or the value it points to in this case will be a compiler error!
```
