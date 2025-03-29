### Syntax
```c++
protected
```
### Privacy
### Example
```c++
struct a_struct {
private:
	int private_member;
protected:
	int protected_member; // member is now inaccessible except to friends and any child classes
public:
	int public_member;
}
```