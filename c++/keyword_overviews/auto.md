### Syntax
```c++
auto identifier;
type-constrait(optional) decltype(auto)
```
### Storage Specifier
Used as a placeholder for the compiler to work out types of expressions. Originally this specifier was shorthand for [[int]].
### Example
```c++
int a = 4;
int b = 3.0f;
auto c = a + b; // compiler determines the type of the  = expression by looking at a + b, then uses that result to set the type of c
```
