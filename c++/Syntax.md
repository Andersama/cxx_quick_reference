C++'s syntax is a series of expressions or declarations, they define structures, functions, or variables and how they are used in the program.

```c++
// A set of //'s starts a single line comment
/* A /* starts a multiline comment, they are not nested, they end with */
/* C++ makes use of the same preprocessor from C, lines that start with # and an identifier may be a preprocessor directive, preprocesor directives function as though they replace text */

// This include directive searches for header files in the compiler's directory
#include <iostream>

// A define directive can be used to make text replacements
#define MYHEADER 0
// An if directive can be used to selectively add/remove blocks of code
#if MYHEADER
// This include directive searches for "myheader.h"
#include "myheader.h"
#endif

/*
The building block of the recognizable parts of c++ grammar as with many other programming languages are identifiers. Identifiers start with letters a-z or an _ and then may include numbers 0-9. Certain identifiers are keywords, these keywords are protected by the compiler and may not be redefined.
*/

// This is a function prototype, or a "forward-declaration".
// This tells the compiler that the following function exists, even if it's not been defined yet.
int main(int argc, const char **argv);
// Declarations are statements, we use ; to mark the end of a statement.
// This declaration states, there is a function called main, it returns an int and takes an input of an int (called argc) and a const char** (called argv). Forward declarations of functions do not need to name the parameters for the compiler to understand how to use the function! It's the order in which the parameters are given which defines how they're used.

// C++'s grammar doesn't particularly care about whitespace, feel free to use spaces, tabs or entirely new lines to format your code as you like.

// This is a function declaration, it includes a function signature
int main(int argc, const char **argv)
{ 
	// and a function "body" surrounded by {}.
	// Inside a function we can define variables.
	// Variables are defined by a type and an identifier.
	int a = 0;
	
	// When declaring a variable you may modify the type by using specifiers.
	// Specifiers change the compiler's understanding about the usage of the variable.
	const int b = 1;
	// The const specifier tells the compiler we expect b to remain constant.
	// Attempting to modify b from this point forward or using b in a non-const manner will result in a compiler error, there are a number of specifiers.

	// In this example we've "initialized" a to 0 and b to 1.
	// The program assumes we progress step by step, you can read the code from top to bottom and for the most part left-to-right.
	
	a = 3; // This is an assignment statement, a is now 3!
	a++; // This is an increment statement, a is now 4!

	// To perform repetitive tasks we can make use of a loop
	for (int i = 0; i < argc; i++) {
		std::cout << i << '\n';
	}

	return 0; // We can end a function and pass along an result
} // Although a function definition is a statement, because it ends with a recognizable {} pattern, the compiler won't require you to end it with a ;
```