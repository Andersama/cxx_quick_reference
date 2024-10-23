### Syntax
```c++
protected
```
### Privacy
### Example
```c++
struct a_struct {
private:
	int private_member; // member is now inaccessilbe except to friends
protected:
	int protected_member;
public:
	int public_member;
}
```