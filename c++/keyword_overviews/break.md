### Syntax
```c++
break
```
### Control Flow
Exits out of a loop or other code execution.
### Example
```c++
int sum = 0;
for(int i = 0; i < 100; i++) {
	sum += i;
	if (i == 50)
		break;
}
// sum is now the sum from [0,50]
```
