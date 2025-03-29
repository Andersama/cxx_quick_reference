```cpp
// <- Starts a single line comment
/* <- Starts a multi line comment
      Ends a multi line comment -> */

// Lines starting with # are preprocessor directives
#include "header.h" // This is the include directive, it expects a filename, the compiler will typically be told on the command line where include directories live
#include <string>   // This is another version, <>'s tell the include directive to search the language's directory for libraries first

// C/C++'s include directive behaves AS-IF the targetted file were copy/pasted at that location! It does not care about the extension of the file (.h) although .h and .hpp are fairly standard to see.

// There are MANY preprocessor directives, so here are a few common ones
#if 1
// starts a conditional preprocessor block, expects a macro 
#elif 0
as with many languages the preprocesor can chain conditional expressions with an else if
#else
the contents of conditional preprocessor blocks which are NOT taken are NOT used for compilation, and so
if the contents were not legal C/C++ they will not produce errors
#endif

#define AMACRO 0
//defines a macro, think of macros as programmable text replacement
#undef AMACRO
//undefines a macro, there's no problem undefining a "non"-existant macro
#ifndef AMACRO
//this block would be included
#endif
//ifndef is short for #if not defined()

//NOTE: Preprocessor defintions can be provided on the command-line, this is how many C/C++ libraries adjust their functionaltiy to suit different
//machine architectures and features! There are also several macros that are expected for the compiler to define.

//NOTE: Because of the behavior of the #include directive and C/C++'s very strict typing and one-definition rules most headers will have a "preprocessor gaurd"
// which disables the header's contents from appearing more than once! This is because many headers will include other headers, protentially including the same ones without
// the user of the header noticing!

// A preprocessor gaurd will typically look like this:
#ifndef A_VERY_SPECIFIC_MACRO_NAME
#define A_VERY_SPECIFIC_MACRO_NAME
// Contents of the header!
#endif

// Or:
#pragma once //At the start of the header file, pragma is a very weird preprocessor directive, it has many uses. #pragma once was introduced as a convienient way to do the
// above without the risk of someone else accidentally creating a conflict with a matching preprocessor macro.

// C++ does not care about whitespace, parts of the language can be spaced out across lines.
int // and can EVEN be broken up with comments (comments are considered whitespace!)
	a // is an "identifier", identifiers are used ~everywhere~, they're essentially how the compiler keeps track of variables, functions, and other defintions, it's just a name
	= // = is an "operator", these take operands on the left and/or right hand side of the operator to perform special functionality, = is assignment
	1 // 1 is a "literal", literals are special to the compiler because they're an "expression" with an implicit type attached and cannot be modified
	; // since "expressions" can be stretched out across lines, c++ uses ; to terminate expressions. Expressions which would "execute" code are often called "statements". 
// a = 1 is an "assignment expression"
// int a = 1 is an "assignment expression" or "variable declaration"
// int a = 1; is an "assignment statement"

1 * 9; // this is technically legal C/C++ code, but has literally no effect, since the expression will not modify any memory its result will be discarded, and therefore
// its whole execution can be ignored. One of C++'s benefits is that it only has you "pay" for what you use. It will optimize a lot away.

int b = 1 * 9; // but here, as an example now that we've taken the result of that expression and assigned it to a piece of memory named "b", the compiler will have to work just
// a bit harder to potentailly remove this expression, because now it must make sure the resulting "b" is never used.

const char *str_like =
	"a string" // we've seen this already a couple times, this is a "string" literal, this constructs an array of characters in memory terminated by a 0
	;

const char also_str_like[] // this is an array declaration, this is secretly equivalent to the statement above, when declaring an array a size is normally expected.
	// It may be a calculated expression, but if so, it must be one that can be evaulated at compile time (EG: the result must be a constant expression)!
	//EG: [9], but here because the size can be deduced from the intialization expression on the right hand side we can leave it unspecified and let the compiler figure it out
	= {
		'a' // this is a character literal, these are NOT arrays, this is an integral expression (an integer) and therefore NOT terminated by a 0
		,' ','s','t','r','i','n','g',0};

// This is a struct definition
struct return_type {
	
};

// This is a class
class parameter_type {

};

// To the compiler structs and classes are equivalent! They define the memory layout of data that will be
// used in the program, these are called "types". The only difference is convienience for the writer, or library designer.
// structs assume all members are public. structs are a carry-over from C, so they have identical behavior.
// A "class" is "new" to C++, C++ used to be called C with classes. They assume all members are private by default.

// You can imagine that "classes" look a bit like this to the compiler by default
struct behind_the_scenes_example {
private: // This line changes the privacy (called the access mode) of all the following members, there are 3, private, public and protected
	// Everything you'd otherwise write
protected: // You can change the access mode at any given point in a type's declaration
private: // Including back to another, this might be because some members should have different access modes, but also should be defined
	// in a particular order!
public:
	int   a; // This is a variable member declaration, it says "behind_the_scenes_example" has a variable named "a" which is an int
	char  b; // The declaration order is important, this determines the memory layout, here a comes before b and b before c
	short c; // By default any variable declaration assumes the variable is "aligned".
	
	// Alignment refers to the fact that on most hardware the actual computer instructions are somewhat restricted
	// to particular memory addresses! 
	// EG: On most hardware an "add" instruction for 32 bit wide integers will need 4 byte alignment.
		//(32 bits / 8 bits in a byte = 4 bytes).

	// Addresses in memory are typically byte addressable, meaning that address 0x1, refers to the second byte, 8 bits in.
	// To satisfy the alignment requirement of the instruction the integers would need to be divisible by the alignment with no remainder.
	// EG: Any 32 bit integers would need to be located at (potentially) address 0, 4, 8, 12 etc...
	// If* the values of the integers were "unaligned", this typically would complicate the process to perform the addition, normally
	// this would mean that additional instructions would be used to manipulate the data either back into alignment, or an "unaligned" instruction
	// might be used (which may incur a performance penalty, where you can imagine that extra steps are being performed to "align" the integers).

	// Because we're ordering disparate types of different alignment, the compiler will do us the favor of ensuring that the resulting addressess
	// will always satisfy ALL of the members alignment requirements. This is accomplished by adding "padding", spacing members additional bytes
	// apart from one another.

	// The compiler accomplishes this by processing the members in order, satisfying the alignment requirement of each in turn.
	// It does this by assuming the struct as a whole must be aligned. The simplest way to picture this is that we're starting on address 0.
	// This is because address 0 satisfies ~any~ alignment requirement.

	// EG: In this example, first the compiler sees "a", an int. Because the struct must be aligned, it will assume the first member is aligned.
	// Then it will try to determine where "b" should go. To do this, the compiler keeps track of the addresss which have been used. Since it started
	// at address 0, and placed a 4 byte variable, it can now assume it is working from address 4 as 0-3 have been taken.
	// We can picture this as just adding the size of the type to a running count.
	// Now it sees "b", a char, which has an alignment of 1. The address 4 / 1 = 4 remainder 0, so it can be placed at address 4. The compiler adds the size of
	// the type (1) to the running count (now 5), and moves on. NOTE: an alignment requirement of 1 essentially means the data could be placed anywhere!
	// Now it sees "c", a short, which has an alignment of 2. The address 5 / 2 = 2 remainder 1, so "c" cannot be placed at address 4. The compiler then adds
	// enough bytes to satisfy "c" (2-1) to the running count (now at 6). Now "c" can be placed at "6". Then "c"'s size (2) is added to the running count, now (8).
		
	// Lastly after all members have been aligned, the compiler must garuntee that the struct itself when placed "contiguously" in memory will remain aligned.
	// This is done by keeping track of the maximum alignment requirement of all of the members (here 4), adding padding to the end of the struct if needed.
	// 8 / 4 = 2 remainder 0, so no padding is needed at the end of this struct!.
};

// We can ask the compiler details about types, including their size and alignment!
int alignment_example = alignof(behind_the_scenes_example); // will return 4
int size_example = sizeof(behind_the_scenes_example);  // will return 8

// We can force the compiler to use a completely different alignment, if we chose one that is smaller this is called "packing"
alignas(2) struct non_standard_alignment {
	int thing_4;   //at offset 0 (same as normal)
	short thing_2; //at offset 4 (same as normal)
	int thing_4_2; //at offset 6 (would otherwise be at offset 8!)
};

// For performance reasons it's good practice to place members which are used often together, and ones which are used
// more often towards the start of the struct. This is because calculating the offset to the first variable in a struct is the equivalent to 
// knowing where the struct is placed (an offset of 0 requires no additional mathmatical operations to properly address it).

// These are to reduce spacial (memory wise) and temporal (time) locality, improving performance by keeping data which is often used
// in caches. Caches are often lower latency and higher throughput forms of memory with limited space automatically managed by
// and built in to the cpu.

// Where structs look like this
struct behind_the_scenes_struct_example {
public:
	// Everything you'd otherwise write
};

// The privacy level of a member determines where it can be used:
	// public: anywhere by any instance of the type (children included).
	// protected: can be used by children of the type internally, but otherwise is private.
	// private: only by an instance of the type internally.

// Changing the privacy level is useful for library designers to prevent accidental missuse of the library.
// Many C++ libraries will make variable members private, and only allow modification of the type through member functions.
// However* it is often more performant to allow direct modification of members as it is more challenging for the compiler to optimize functions.

template<typename A> // This is the start of a template*, templates can be a bit recursive although this is rare!
template<class B> // This would create a template of a template, normally this is done where B and/or following types would be calculated from A*, or is otherwise very complicated. typename and class are equivalent here
return_type templated_function_name(parameter_type parameter_name) { // Templates can be used for many things, including functions.
	// Functions have a return type, this type may be templated, or even deduced by the compiler!
	// The more we specifiy for a templated declaration the less work the compiler will have to do to deduce how it is used.
	// If the compiler cannot determine all the necesssary components for a template from its usage, it will produce an error!
	return; // It will also produce an error if a return type is specified but a return statement cannot be converted to the correct type.
}

template<class T,
	size_t N> // Templates may have more than one template parameter, and newer standards of C++ allow templated and typed constant expressions!
struct our_own_carray {
	T data[N];

	our_own_carray(const char *str) {
		size_t i = 0;
		for (; str && *str && (i+1) < N; ++i) {
			data[i] = str[i];
		}
		data[i] = 0;
	}
};

// To use templates, we provide the template parameters between <>'s after the template's name (identifier).
our_own_carray<char,9> deja_vu = "a c-string";

// Because no one is original, and names might otherwise overlap between one library writer and another, C++ also provides "namespaces".
namespace my_definitely_original_namespace {
	// Anything defined or declared inside of the {}'s will essentially be prefixed with the namespace.
	int variable = 0;
}
// To access something inside a namespace explicitly, the "scope" :: operator is used.
my_definitely_original_namespace::variable += 1;

// However, as with templates, the compiler will try to deduce anything you're using.
variable += 1;

// So long as there isn't a conflict with something else, namespaces don't have to be provided.
// However it is good practice to explicitly use namespaces to avoid problems.

// If typing out namespaces is tiring you can hint to the compiler which namespaces to give priority to search through with a using expression.
using namespace my_definitely_original_namespace;
// WARNING: Doing this OUTSIDE a scope, such as the body of a function or a type definition will "LEAK" the namespace
// potentially creating a whole slew of compiler errors. As the compiler erronously looks through or uses the newly prioritized
// namespaces in places it shouldn't.

variable += 1; // The compiler won't necessarily treat this as an error even with a conflict, unless another namespace with a matching
// priority is found.

// NOTE: In C / C++ you may need to "prototype" functions or types, this is to give the compiler
// a heads up that a function or structure exists, but may not have been defined yet.

struct a_prototyped_struct; // A prototype will look like a structure or function definition.
	// It will be missing the body/definition (the content that belongs in {}'s).
	// This may also be called a forward declaration.

// The prototype MUST be defined at some point (otherwise this is a compiler error).
struct a_prototyped_struct {

};

// This is because you may run into cases where two or more structs may need to be aware of one another
// but the compiler would otherwise panic about a missing definition.

struct a_cyclic;
struct b_cyclic;

struct a_cyclic {
	b_cyclic error_variable; // If such a need arises, be aware that you need to avoid cyclic definitions.
	// Here since the size of a_cyclic depends on b_cyclic which depends on a_cyclic the compiler will panic!

	b_cyclic* ok_variable; // We can get around this using pointers, since the size of a pointer is constant.
	// Pointers solve this issue since the compiler does not need to know the size or alignment or anything else
	// about b_cyclic, a pointer is simply an address, which is a number!
};

struct b_cyclic {
	// Forward declarations can be made essentially anywhere by using struct or class where a type belongs.
	struct a_cyclic* ok_variable;
};

int func(struct a_cyclic* ptr, struct b_cyclic* ptr_2); // You will often see this in function prototypes

// In C++ functions look like they would in C
int main(int argc, char **argv) {
	// First we tell the compiler the return type of the function (int) and its specifiers (const etc...)

	// Second we give the function its name (must be an identifier)
	// identifiers start with _ or an alphabetical character, and then may be followed with more and/or numbers
	// main_0 is an identifier where 0_main is not
	
	// Then we provide a list of parameters inside ()'s
	// Lastly we provide the actual code that will be executed in {}'s this is the body or definition
	// of a function

	return 0; // Functions must return, if they have a return type other than void specified they must return
		// an expression which is castable to the provided return type.
		// "Casting" is C/C++'s term for transforming one piece of data of one type into another. 
		// Here we return a literal 0, which is an an int, no casting required.
}

// The simplest function, takes no arguments
void do_nothing() {
	return; // and returns from the function
}

// At the lower level (in assembly / machine code), the return value is placed in a reserved register.

// Registers are the smallest and fastest memory unit (not addressable in code) where all the work by
// the CPU is performed.

// Functions are blocks of code where parameters are provided in registers.
// The exact registers which will get used are specified by the "calling convention".
// C as a language has its own calling convention, as does C++!

// In order to "call" a function registers are essentially "saved" for later, allowing the function
// to make use of the registers inside the function.

// When a function "returns", the CPU restores the saved registers, dedicating a specific register
// for the function's "result" (not restored, modified by the function).

// This is why C is so popular / prevelant as a compiled programming language. When another language
// would want to "call" a function compiled using C, the function signature is enough to know
// exactly how to do so. And since C is easy to read / process, it's also trivial to incorporate directly.

// C++ however is not easy to "call", this is an unfortunate consequence of a C++ feature called overloading.

struct using_a {};
struct using_b {};
struct using_c {};

// Overloading is the C++'s ability to distinguish function calls by deducing and distinguishing between types.
int do_thing(using_a thing1, using_a thing2);
int do_thing(using_b thing1, using_b thing2);
int do_thing(using_a thing1, using_b thing2);
int do_thing(using_b thing1, using_a thing2);

int example() {
	using_a a_example;
	using_b b_example;

	do_thing(a_example, a_example); // Each of these lines will call a different function!
	do_thing(b_example, b_example);
	do_thing(a_example, b_example);
	return do_thing(b_example, a_example);
}

// In essence, this is accomplished by C++ secretly including the WHOLE function signature as the "name" of the function.
// In C the "do_nothing" identifier IS the "name".
int do_nothing(using_c thing1, using_c thing2);
// and so introducing another signature with the same "name" would result in an error!
int do_nothing(using_c thing1, using_a thing2);

// The process of creating a "name" for C++ to actually call is called "name mangling", and is fairly complicated.
// Details can be found here: https://en.wikipedia.org/wiki/Name_mangling
// The unfortunate aspect is that unlike C where the name is trivial to determine, it takes a full-fledged C++
// parser to extract the proper mangled C++ name. To compensate for this, C++ allows functions to be exported
// using C's naming convention. Allowing developers to write functions in C++, but still provide the flexibility
// of having other languages or libraries use the resulting binaries in a trivial manner.

// NOTE: This special behavior is completely backwards compatible with C, so only
// ONE definition of a function with any given name is meant to be present.

// For this reason you may find code wrapped in preprocessors like so:
#ifdef __cplusplus
extern "C" { // Hints to a C++ compiler the following was written in C, so the compiler should assume C's calling conventions etc...
	// We only need to export C interface if
	// used by C++ source code
	// __cplusplus will be defined by any C++ standard compiler
	#endif

	
	// We can always manually set the calling convention ourselves, however it's much easier
	// to let the compiler do that for us and contextually too.

	// EG: If this block of code were included into a C compiler, it would ignore the extern "C" { } block
	// and would be taken as external C functions meant to be loaded in by a DLL
	__declspec( dllimport ) void MyCFunc();
	__declspec( dllimport ) void AnotherCFunc();

	// Whereas in a C++ compiler the extern "C" { } block is not ignored, hinting to the compiler
	// that these function's names are meant to be left unmangled.

#ifdef __cplusplus
}
#endif

// Or headers wrapped like so:
extern "C" { 
	#include "MyCHeader.h"
}

/* Now for a tutorial */
#include <iostream>

int a_global = 0; // Variables defined outside of a function or a type definition are part of the "global" scope.
// To "compile" a program we must provide a start function, in C/C++ this is "main".
// "main" can have several function signatures that are all acceptable to the compiler.

static int a_static_global = 0; // Static variables are only accessible to the file where they are defined*

int global_example() {
	a_global += 1;
	return a_global;
}

int static_example() {
	static int a_static = 0; // Static variables inside a function are really "global", where the intialization statement
	// will be skipped after the first succesfull exectuion.
	a_static += 1;
	return a_static;
}

int main(void) {
	// void is interesting as a parameter, technically it's meant to tell the compiler that ANY
	// number of parameters may be being passed to the function!
//int main() { // This is also ok, a parameter list with nothing in it means NO parameters are expected.
//int main(int argc, const char **argv) { // "main" with parameters takes a count and a list of c-strings as arguments.
//int main(int argc, const char **argv, const char **envs) { // you may also see a second list of c-strings passed, these are the "environment variables".
//NOTE: This is environment variable PATH on windows appended with the "user"'s PATH.

	int a_local = 0; // Variables defined inside of a function or a type definition are part of a "local" scope.

	// functions introduce a "scope", a scope begins at the { and ends at a return expression or a }
	// A scope provides a rough guide for determining the "lifetime" of a variable.

	// Here a_local is an integer, whose lifetime ends as the function terminates with a return.
	{ // C++ allows scopes to be introduced at any time, these are called "compound statements".
		int a_local = 1; // NOTE: C++ is weird, it allows names of variables to be "shadowed".
		// That is the name of a variable is tied to its scope, so when
		a_local += 1; // executes
		
		// std::cout is a global variable with a type with an overloaded << (left shift) operator. It uses <<
		// to "stream" of the variable on the right hand side, and returns itself so that <<'s can
		// be chained together to output more. cout is short for console output, its will be displayed in a
		// console window if available. Using std::cout will "stream" the output to a "pipe", this is how
		// console applications can take the input of one program and process it in another.
		std::cout << a_local << '\n'; // the a_local here refers to the one inside this scope which was 1 and now is 2
	} // this newly introduced a_local will be destroyed here.

	std::cout << a_local << '\n'; // Where a_local here refers to the value which we set as 0 at the very top!
	
	// So be careful with scopes and shadowing variables, this can make code confusing.

	// NOTE: Wrapping code with {}'s is convienient for copy/pasting code! Since any variables introduced won't
	// impact the parent scope.

	// Globals can be accessed in any function, and so they might be modified in any function.
	a_global += 1;
	global_example();
	std::cout << a_global << '\n'; // a_global *might* display 2 here
	// Due to the nature of globals being acessible anywhere external libraries sharing globals can create
	// confusing problems with execution order. Since globals must be safely used anywhere they
	// actually are "created" BEFORE main! This code is usually placed in randomly named but dedicated function, which
	// the programmer will never be able to manually call themselves. This function typically is part of what
	// handles loading any external dependancies. This means however that dependancies MAY modify global
	// variables before main ever executes.

	static_example();
	std::cout << static_example() << '\n'; // his will display 2
	// the first call sets the static variable to 0 and then increments it to 1
	// the second call sets the static variable to 2.

	return a_global;
}

// Because []'s of unspecified length "decay" to pointers you may see main defined like:
// int main(int argc, const char *argv[], const char *envs[]);

// Globals (and statics) will not be destroyed until the program is about to terminate.

template<size_t N>
auto an_odd_cout_example(const char (&incoming_array)[N]);
// The ()'s surrounding &incoming_array are necessary to specifiy
// a template on a c-array. This in because without the ()'s the type reads as an "array of const char references", where an array of references is NOT allowed.
// What we were after was a "reference to a const char[N]". Forgive C++ for this mess, it's because parsing the language can be a mess and sometimes
// strange things like this are the work around.

#include <iostream>
int main_pointer_example(int argc, const char** argv) {
	// When programming it is important to be able to work with pointers
	// const char ** -> is a pointer to a pointer to a const char
	// pointers store addresses to memory. C/C++ allows specifiying what types pointers point to
	// in addition to whether the pointer itself may be modified or the pointed to location may be modified
	// they can be nested as argv is above.
	if (argc > 0) {
		// To access the contents of a pointer we may do the following using the array access operator []
		const char* chr_ptr = argv[0];
		// The array access operator performs pointer arithmetic, returning a new pointer offset properly
		// by the size of the underlying type.

		const char* chr_ptr2 = *(argv + 0); // We can imagine the above line is equivalent to this expression.
		// * when used as a unary operator is the "dereference" operator, this tells the compiler that
		// we intend to take the contents of a register and treat it as an address to load another location
		// from memory into another address.
		// When something is "dereferenced" think "loaded".
		
		// Dereferencing effectively removes one * from the type.
	}

	const char chrs[] = "A simple decaying example";
	// Because C doesn't include "size" information with "arrays", C "decays" arrays to the address
	// of the first item in the array.
	const char *chrs_ptr = chrs; // This makes the following expression "OK", since chrs "decays" into a const char* behind the scenes.
	// NOTE: While C doesn't include the size information with the arrays, C allows the programmer
	// to query the size of an array at any given point using sizeof().
	size_t number_of_chars = sizeof(chrs) / sizeof(const char);
	// C++ keeps this behavior, HOWEVER C++ will maintain the original type so that template functions can extract the 
	// size as part of the template's body.
	an_odd_cout_example(chrs) << '\n';

	return 0;
}

template<size_t N>
auto an_odd_cout_example(const char (&incoming_array)[N]) { 
	std::string_view vw { incoming_array, N };
	
	if (N & 0x1)
		std::cout << "An odd string\n";
	else
		std::cout << "An even string\n";

	// References are indicated by a '&' following a type, except in the unusual case above where we hint to the compiler the reference is to be read after using ()'s
	// Consider references to be pointers, with a special caveat:
		// 1) References, unlike pointers MUST be initialized.
		// 2) References, because they MUST point somewhere, do not need to be "dereferenced" to use the underlying value.
	std::string_view &vw_ref = vw; // Read this as vw_ref references vw, EG: the reference is assigned a pointer to vw!
	return std::cout << vw_ref; // In short: References are used as if they weren't pointers at all!

	// References have several special benefits, because they point somewhere, references "never" need to be checked if they are NULL.
	// In addition in many cases, although the implemention of a reference is simply a pointer, a reference MAY be
	// treated as an alias of the referenced variable, this may ignore the cost of a pointer entirely.
	// This function is an example where that may be possible because vw_ref is not returned.

	// In scripting languages like javascript saving the result of accessing variables that are used often can be thought
	// of as taking a "reference" in C++. Saving the effort of processing the work need to reach a particular address.

	// Although C++ tends to be highly optimized, this type of reuse of an already calculated address, can be expressed
	// directly with references.
}

// When returning a struct C/C++ may opt to use a pointer to a memory address with
// the contents of the result as opposed to the value depending on the size of the type.
// This will not be "visible" in the code itself.

// Returning a "reference" is of course to C++ the same as returning a "pointer", however you must
// be careful of the lifespan of references and the things they reference if you do so!

int & referencing_a_bad_time() {
	int a = 4;
	int &b = a;
	return b; // Oh dear..., b references a, but a is going to be destroyed! What does b really point to now?
}

// Modern C++ may extend the lifetime of variables it detects are used in this awkward way. But don't count on it...it's a bad idea in general,
// and is otherwise a fantastic way to introduce REALLY weird bugs.

// ~ Congratulations! ~ You've read through the entire quickstart guide on C++!
```