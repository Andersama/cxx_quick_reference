### Syntax
```c++
for (initial-statement; boolean-expression; step-statement) compound-statement
for (range-declaration : range-expression) compound-statement
```
### Flow Control
For loops are used to execute code repetitively, they can run indefinitely or be limited by a fixed count.
### Example
```c++
#include <vector>
#include <iostream>
```

```c++
std::vector<int> numbers;
for (int i = 0; i < 100; i++)
	numbers.emplace_back(i);
for (const int& num : numbers)
	std::cout << num << '\n';
```