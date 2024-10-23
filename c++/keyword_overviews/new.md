### Syntax
```c++
new type-expression
```
### Memory Management
The new expression will call an allocator to retrieve memory that can store the type specified by the type-expression, as well as the type's constructor. This function is responsible for retrieving memory to be used by the current program. This is used in conjunction with [[delete]].
### Example
```c++
int *ptr = new int(); // allocate an integer
*ptr = 5;
delete ptr; // return the memory back via its destructor
```