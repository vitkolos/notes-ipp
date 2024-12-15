# CS 106L: Standard C++ Programming

- struct – bundle multiple variables into one type
- using – set an alias to a type
- auto – compiler deduces the type of the expression
- initialization
	- direct initialization
		- `int a = 42.5;`
		- `int a(42.5);`
		- does not check the type, simply stores 42
		- narrowing conversion
	- uniform initialization
		- `int a{42.5};`
		- does not allow for narrowing conversion, the compiler generates an error
		- ubiquitous – works for all types
- structured binding
	- `auto [x, y, z] = f();`
	- can be used on objects where the size is known at compile-time
- reference
	- pass by value × pass by reference
- l-value, r-value
	- l-value can be to the left or the right of an equal sign
	- r-value can be only to the right of an equal sign
- const
	- you can't declare a non-const reference to a const variable
- streams
	- stream = a general input/output abstraction
	- stringstreams
		- useful when mixing data types
		- `>>` operator reads until the next whitespace
		- `getline()`
	- output streams
		- buffered
			- `std::flush` or `std::endl` can be used to flush
			- flush is expensive → it might be better to use `\n` (and `std::ios::sync_with_stdio(false);`) instead of `std::endl` if we want to use it repeatedly
		- `ofs.open("hello.txt", std::ios::app);`
			- `std::ios::app` … append flag
	- input streams
		- also buffered
		- `>>` operator on cin reads until the next whitespace
		- `getline` reads the whole line
		- they should not be combined
- standard template library
- containers
	- sequence containers
		- vector
		- deque
	- associative containers
		- map, set
			- using comparison
		- unordered_map, unordered_set
			- using hashing
- iterators
	- streams don't allow multi-pass iterators
	- special syntax
		- `(*it).x` ~ `it->x`
		- `*(it+5)` ~ `it[5]`
	- pointers work similarly to iterators
- classes
	- structs are like classes but everything is public there
	- fields
	- constructor
	- member functions
	- destructor
	- fields and headers in `.h` file (or `.hpp`?)
	- `this` pointer
	- `using` … type aliasing (e.g. iterator)
- inheritance
	- dynamic polymorphism
		- virtual functions
	- inheritance visibility (public, protected, private)
	- virtual inheritance
		- to avoid diamond problem (`B:A`, `C:A`, `D:B,C`)
		- derived class (D) needs to initialize the base class (A)
			- in initialization list (?)
- templates
	- separation of headers and implementation might be problematic
		- should be in the same file
	- `template <typename T>` ~ `template <class T>`
	- (partial) specializations
- const methods
	- instead of `T* this`, they can use only `const T* this`
	- const overloading
		- `const T& at(size_t index) const;`
		- `T& at(size_t index);`
	- const party tricks
		- `const_cast` … casts away constness
		- `mutable` … marks field as mutable even in const instances
- templated function
	- implicit × explicit instatiation
- concepts
	- example

```cpp
template <typename T>
concept Comparable = requires(const T a, const T b) {
	{ a < b } -> std::convertible_to<bool>;
};
```

- concepts (cont'd)
	- everything in the curly braces must compare without error and the result must be bool-like (convertible to bool)
	- usage
		- `template <typename T> requires Comparable<T>`
		- shorthand: `template <Comparable T>`
- recursion using variadic templates

```cpp
template <Comparable T>
T min(const T& v) { return v; }

template <Comparable T, Comparable... Args>
T min(const T& v, const Args&... args) {
	auto m = min(args...);
	return v < m ? v : m;
}
```

- compile-time code execution
	- template meta-programming
	- `constexpr` … expression should be evaluated at compile time
	- `consteval` … expression must be evaluated at compile time
- passing predicates/functors
	- global functions can be passed as functors
		- actually, thay are passed as function pointers
		- `bool isVowel(char c)` is passed as type `bool(*)(char)`
	- lambdas
		- can capture context
		- by reference / by value
	- functor … any object that defines `operator()`
- range
	- everything with begin and end
	- instead of `std::find(v.begin(), v.end(), x);` for vector `v`, we can use `std::ranges::find(v, x);`
- view
	- range that lazily transforms its underlying range, one element at a time
		- see `std::ranges::views` and `std::ranges::to`
		- first parameter … underlying range
	- alternative: range adaptors
		- omit the range parameter
		- pipe `|` operator
	- note
		- `std::ranges` algorithms are eager
		- `std::ranges::views` are lazy
- operator overloading
	- member × non-member
	- we can use friend declaration to provide access to private fields
- special member functions
	- 6 SMFs
		- default constructor
		- destructor
		- copy constructor
		- copy assignment operator
		- move constructor
		- move assignment operator
	- generated (if not explicitly defined) only when they're called
	- constructor
		- using initializer lists is more efficient, we can directly construct member variables with intended values
	- copy constructor
		- by default, it creates copies of each member variable
		- if there is a pointer in member variables, the memberwise copy will point to the same allocated data
			- we need to define custom copy constructor
		- what if we want prevent copying?
			- just set the functions equal to delete
		- also, we can set the SMFs equal to default (this might be necessary in some cases)
		- rule of zero: if the default SMFs work, don’t define your own
		- rule of three
			- if you need a custom destructor, then you also probably need to define a copy constructor and a copy assignment operator for your class
- move semantics
	- rvalues are automatically (?) moved
		- `Photo retake(0,0);`
		- `retake = takePhoto();`
		- does not copy the result of takePhoto, only moves it
	- what if we want to pass the value to the function and expect the value disappears in the function
		- if we wanted to use `&` reference, we would need to assign an address to the value first
			- `Photo selfie = takePhoto();`
			- `upload(selfie);`
		- if we use `&&` reference, we don't need to do so
			- `upload(takePhoto());`
	- move constructor, move assignment operator
	- `std::move` casts an lvalue to rvalue
	- rule of five: if we defined copy constructor/assignment and destructor, we should also define move constructor/assignment (to prevent unnecessary copying)
- `std::optional<T>` can hold `std::nullopt` or a value of type `T`
	- there is no `std::optional<T&>` :((
- RAII … Resource Acquisition is Initialization
	- resources used by a class should be acquired in the constructor and released in the destructor
	- lock & unlock → lock_guard
	- new & delete → smart pointers
