### Syntax
```c++
private
```
### Privacy
### Example
```c++
struct a_struct {
private:
	int private_member; // member is now inaccessible except to friends and child classes
protected:
	int protected_member;
public:
	int public_member;
}
```