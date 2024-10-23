### Syntax
```c++
continue
```
### Control Flow
Jumps to the step expression of a loop or other code execution.
### Example
```c++
int sum = 0;
for(int i = 0; i < 100; i++) {
	if (i == 50)
		continue; // jumps to i++, ignores adding 50 to the sum
	sum += i;
}
// sum is now the sum from [0,50) + (50, 100) or [0, 100) - 50
```
