### Syntax
```c++
concept identifier = requires-expression
```
### Usage
Defines a constraint that a type must match to satisfy a "concept". Concepts are used to restrict which types can be used in a template.
### Example
```c++
// An example from cppref
template<typename T>
concept Hashable = requires(T a)
{
	// a type that is "Hashable"
    { 
	    // must be able to be used via this expression
	    std::hash<T>{} (a)
    }
    // and the resulting type of that expression must be a type which is convertible in some way to std::size_t
    -> std::convertible_to<std::size_t>;
};

// A template function which is constrainted to types which are "Hashable"
template<Hashable T>
void f(T) {}

```