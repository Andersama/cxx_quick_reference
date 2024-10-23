### Syntax
```c++
delete expression
```
### Memory Management
The delete expression will call a type's destructor, this function is responsible for releasing memory to be used for other purposes by the operating system or the current program. This is used in conjunction with [[new]]. The expression must represent some form of pointer type.
### Example
```c++
int *ptr = new int(); // allocate an integer
*ptr = 5;
delete ptr; // return the memory back via its destructor
```