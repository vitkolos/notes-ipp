# Programming in C++

- header files in C++
	- the whole class has to be in the header file (including implementation of the member functions, even private members)
- it is not a good idea to try to modify the value of a function parameter
- when using `const` and pointers together, it might get complicated
	- the behavior will differ based on the `const` keyword position
- function declaration vs. definition
	- declaration – in the header (hpp) file
		- does not have to contain names of the parameters
		- can contain default values of the parameters
	- definition – in the source (cpp) file
- `inline` keyword
- if you insert something in a container, it is copied
- `const` keyword
- `auto&&` → compiler will determine the best way to access the item (might even use const)
