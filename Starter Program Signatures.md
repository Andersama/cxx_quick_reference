```c++
#include <iostream>
```

```c++
// Program that expects no input arguments
int main() {
	return 0;
}

// Program that expects no input arguments
int main(void) {
	return 0;
}

// Program expects input arguments
int main(int argc, const char** argv) {
	// argv[0] should be the path of the program itself
	// typically arguments are passed as an array
	// this example assumes #include <iostream> was included at the start
	for (int i = 0; i < argc; i++) {
		std::cout << argv[i] << '\n';
	}
	return 0;
}

// Program expects input arguments, because arrays are passed by pointer
// this is equivalent to the above
int main(int argc, const char*[] argv) {
	// argv[0] should be the path of the program itself
	// typically arguments are passed as an array
	// this example assumes #include <iostream> was included at the start
	for (int i = 0; i < argc; i++) {
		std::cout << argv[i] << '\n';
	}
	return 0;
}

// Program expects input arguments and a list of environment variables
int main(int argc, const char** argv, const char** env) {
	for (int i = 0; i < argc; i++) {
		std::cout << "arg " << i << "\t: " << argv[i] << '\n';
	}
	// unlike arguments, environment variables are passed as a list
	// without a given count we have to check where the list ends 
	int i = 0;
	for (const char** e = env; e; e++) {
		if (*e) {
			std::cout << "env " << i << "\t: " << *e << '\n';
		} else {
			std::cout << "env " << i << ":\n";
		}
		i++;
	}
	return 0;
}
```

### Operating System Specific
```c++
#include <windows.h>
```

```c++
int APIENTRY WinMain(HINSTANCE hInst, HINSTANCE hInstPrev, PSTR cmdline, int cmdshow) {
	return 0;
}

```cpp
int wmain() {
	return 0;
}
// Similar to the standard except uses 16bit wide characters
int wmain( int argc, wchar_t* argv[] ) {
	return 0;
}```
```