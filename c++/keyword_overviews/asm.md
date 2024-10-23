### Syntax
```c++
asm(c-string | raw-string)
```
### Usage
Embeds assembly source code directly into the c++ program.
### Example
```c++
// move the value 42 into the register rax and return using assembly
asm("movq $42, %rax\n"
   "ret")
```