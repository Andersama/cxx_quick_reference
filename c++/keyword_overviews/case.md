### Syntax
```c++
case constant-expression
```
### Control Flow
Defines a location to jump to if the [[constant-expression]] is a match.
### Example
```c++
int value = 2;
switch(value) {
	case 0:
	case 1:
	case 2: //code execution will jump to here
	case 3:
}
```