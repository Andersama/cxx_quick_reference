C++'s syntax is a series of expressions or declarations, they define structures, functions, or variables and how they are used in the program.

```c++
// A set of //'s starts a single line comment, comments are ingored by the compiler
// they are not run as code, in most cases they are considered by the compiler to be whitespace.
/* A /* starts a multiline comment, they are not nested, they end with */
/* C++ makes use of the same preprocessor from C, the preprocessor is responsible for transforming the text before the C++ compiler sees it. Lines that start with # and an identifier may be a preprocessor directive. Preprocesor directives tell the processor when and how to do text replacement to get to a desired source file. */

// For example the include directive searches for files in the compiler's library directory
#include <iostream> // Provides a set of input and output operations to a console.
// You can imagine that the contents of the file iostream are injected in place of #include <iostream>


// You will often use preprocessor directives like these to reuse code throughout your projects. Here are a few common ones
#include <fstream> // Provides a set of input and output operations to files.
#include <vector>  // Provides the standard library's contiguous variable size container. This willl likely be best in terms of performance for many cases.
#include <list> // Provides the standard library's variable size linked list container.
#include <cstdint> // Contains definitions for fixed width integer types.
#include <algorithm> // Defines a number of useful algorithms.
#include <chrono> // Provides a number of time-based operations and structures
#include <array> // Provides the standard library's contiguous fixed size container

// The define directive can be used to make repeated text replacements
#define MYHEADER 0
// This define directive tells the preprocessor to replace any instance of MYHEADER with 0.

// The if directive can be used to selectively add/remove blocks of code.
#if MYHEADER
#include "myheader.h" // This include directive searches for "myheader.h".
#else
	// This comment will end up in the resulting code.
#endif

// The preprocessor above will replace MYHEADER with 0, the #if directive will fail and ignore any text until it reaches #else, #elif or an #endif. Because the if directive failed the #include "myheader.h" will be skipped.

/*
The building block of the recognizable parts of c++ grammar as with many other programming languages are identifiers. Identifiers start with letters a-z or an _ and then may include numbers 0-9. Like many languages certain identifiers are keywords, these keywords are protected by the compiler and may not be redefined.
*/

int main(int argc, const char **argv);
/* This is a function prototype, or a "forward declaration".
This tells the compiler that the following function exists, even if it's not defined yet. Declarations are statements, we use ; to mark the end of a statement.

This declaration states, there is a function called main, it returns an int and takes an input of an int (called argc) and a const char** (called argv). Forward declarations of functions do not need to name the parameters for the compiler to understand how to use the function! It's the order in which the parameters are given which defines how they're used.

NOTE: the compiler processes declarations as it discovers them, so forward declarations are useful when defintions of structs or functions rely on each other.
*/

int process(int arg_count, const char **arg_values) {
	// To use a function, list values you'd like to pass as the parameters.
	// If main hadn't been declared or defined before this point this
	// would be a compiler error!
	main(arg_count, arg_values);
}

// C++'s grammar doesn't particularly care about whitespace, feel free to use spaces, tabs or entirely new lines to format your code as you like.

// Below is a function declaration, it includes a function signature
int main(int argc, const char **argv)
{ 
	// and a function "body" surrounded by {}.
	// Here inside a function's body we can define variables.
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
	++a; // This is a pre-increment statement, this is equivalent to adding 1 to a.
	//a is now 4!
	a++; // This is a post-increment statement, this is equivalent to adding 1 to a, but returning a temporary with a value of 4!
	//but once the expression's been evaluated a will be 5!


	const char *str = "A simple c-string";
	// *'s following a type makes a pointer of that type
	// pointers store addresses of variables, you can have pointers of pointers etc...
	const char arr[] = "Another c-string";
	// []'s following a type creates an array of that type.
	// Both arrays and pointers are used to refer to multiples of a particular type
	// [] normally needs to be filled with a constant to specify the length of the
	// array, however the compiler can deduce the size if the variable is initialized.
	char s = str[0];
	char b = arr[0];
	// C++ borrows from C in that arrays "decay" into pointers, this allows pointers and arrays to share the same "array" indexing operator []
	const char *p0 = arr;
	const char *p1 = &arr;
	// Essentially behind the scenes the expression "arr" will be treated as an address
	// & is the address of operator
	if (p0 != p1) {
		std::cout << "This will never happen\n";
	}
	
	// To perform repetitive tasks we can make use of a loop
	for (int i = 0; i < argc; i++) {
		//a for loop is broken into three distinct parts
		//an intiial statement, eg: int i = 0;
		//a conditional expression, eg: i < argc;
		//and a step statement, eg: i++

		// Before entering a for loop the initial statement is executed
		// Then the conditional expression is evaluated.
		// If the expression is true, we enter the loop's body.
		// If the expression is false, we skip the loop entirely
		std::cout << i << '\n';

		// << is the left shift operator.
		// The standard library defines a template which can handle a number of standard types including int and char. This allows librarys to define custom and easy to use functionality using operators.
		// Here the standard library uses it to write data to an output stream cout (console output).

		// After a loop's body is executed the step-statement will execute
		// then the conditional expression will be evaluated again to see
		// if the program should continue executing the loop.
	}

	for (int i = 0;;i++) {
		// Here the conditional-expression of the loop was ommited, C++ and C consider this to mean that this is a perpetual loop, the "conditional-expression" will be considered to be always true.
		
		// The following is a conditional statement, when the conditional-expression wrapped in ()'s is true it will execute its body.
		if (i < argc) {
			// While in the body of a loop can also tell the compiler to "skip" to the step-statement using continue
			std::cout << i << '\n';
			continue;
		} else {
			// Or we can exit the loop early using break.
			break;
		}
	}

	// A while loop takes a conditional-expression
	while (true) {
		break;
	}
	// This would be equivalent to a for loop with the
	// initial statement and step statement omitted
	for (;true;) {
		break;
	}
	// You might see this in code, this is the shortest way to write an infinite loop.
	for (;;) {
		break;
	}

	int nums[5] = [0,1,2,3,4];
	for (auto num : nums) {
		std::cout << num << '\n';
	}

	do {
		break;
	} while (true);
	// This is a do while loop, unlike for and while loops
	// a do while loop checks the condition at the end of a loop.
	// This means the loop's body is garunteed to execute at least once.

	bool example_condition = true;
	// This initializes a boolean value, it can only store a value of true or false, 1 or 0.
	bool example_condition_1 = true;

	// if's may be chained together like so:
	if (example_condition) {
		// This code would execute if example_condition were true
	} else if (example_condition_1) {
		// This code would execute if example_condition were false and example_condition_1 were true
	} else {
		// This code would execute if neither were true
	}

	int number = 2;
	// switch statements can be used in a simlar fashion to if blocks
	// they take a numerical value and use it to jump to marked locations in code
	swtich(number) {
	case 0: // we mark the locations we want to jump to with cases
		// in C++ once a jump has been made
	case 1:
		// all the following code will execute
	case 2:
		// until we hit a break statement
		break;
	default: // a default case will handle all other values.
		// Unlike if blocks or for loops 
		break;
	}

	{
		int a = 1;
		// So far we've seen many instances of code wrapped in {}'s.
		// This is referred to as a compound-statement in the grammer.
		// Most compound-statments open what is called a new "scope".
		// To the compiler you can consider this a new database or
		// table of variables.
		// This allows C++ to "shadow" variables, or reuse the same
		// identifier without getting confused as to which data is
		// being referred to.
		// This makes wrapping code in {}'s handy for copy-pasting
		// in other locations.
		// However a lot of people find shadowing to be error prone,
		// most compilers will have a warning for "shadowed" variables.
	}
	// switch statements are a rare instance where {}'s don't open a new
	// scope, this is because scopes are used to track when variables are
	// created and when they should be destroyed.
	// This makes switch statements a bit strange because without a scope
	// you won't be allowed to create new variables!
	switch(number) {
	case 0:
	case 1:
	case 2:
	{
		int a = 1;
		// But worry not! As each case expects a compound-statement,
		// so even if the switch doesn't open a new scope you can.
		break;
	}
	default:
		break;
	}


	return 0; // We can end a function and pass along an result
} // Although a function definition is a statement, because it ends with a recognizable {} pattern, the compiler won't require you to end it with a ;
```