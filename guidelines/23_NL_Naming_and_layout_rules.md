### <a name="Rl-comments"></a>NL.1: Don't say in comments what can be clearly stated in code

##### Reason

Compilers do not read comments.
Comments are less precise than code.
Comments are not updated as consistently as code.

##### Example, bad

    auto x = m * v1 + vv;   // multiply m with v1 and add the result to vv

##### Enforcement

Build an AI program that interprets colloquial English text and see if what is said could be better expressed in C++.

### <a name="Rl-comments-intent"></a>NL.2: State intent in comments

##### Reason

Code says what is done, not what is supposed to be done. Often intent can be stated more clearly and concisely than the implementation.

##### Example

    void stable_sort(Sortable& c)
        // sort c in the order determined by <, keep equal elements (as defined by ==) in
        // their original relative order
    {
        // ... quite a few lines of non-trivial code ...
    }

##### Note

If the comment and the code disagree, both are likely to be wrong.

### <a name="Rl-comments-crisp"></a>NL.3: Keep comments crisp

##### Reason

Verbosity slows down understanding and makes the code harder to read by spreading it around in the source file.

##### Note

Use intelligible English.
I may be fluent in Danish, but most programmers are not; the maintainers of my code may not be.
Avoid SMS lingo and watch your grammar, punctuation, and capitalization.
Aim for professionalism, not "cool."

##### Enforcement

not possible.

### <a name="Rl-indent"></a>NL.4: Maintain a consistent indentation style

##### Reason

Readability. Avoidance of "silly mistakes."

##### Example, bad

    int i;
    for (i = 0; i < max; ++i); // bug waiting to happen
    if (i == j)
        return i;

##### Note

Always indenting the statement after `if (...)`, `for (...)`, and `while (...)` is usually a good idea:

    if (i < 0) error("negative argument");

    if (i < 0)
        error("negative argument");

##### Enforcement

Use a tool.

### <a name="Rl-name-type"></a>NL.5: Avoid encoding type information in names

##### Rationale

If names reflect types rather than functionality, it becomes hard to change the types used to provide that functionality.
Also, if the type of a variable is changed, code using it will have to be modified.
Minimize unintentional conversions.

##### Example, bad

    void print_int(int i);
    void print_string(const char*);

    print_int(1);          // repetitive, manual type matching
    print_string("xyzzy"); // repetitive, manual type matching

##### Example, good

    void print(int i);
    void print(string_view);    // also works on any string-like sequence

    print(1);              // clear, automatic type matching
    print("xyzzy");        // clear, automatic type matching

##### Note

Names with types encoded are either verbose or cryptic.

    printS  // print a std::string
    prints  // print a C-style string
    printi  // print an int

Requiring techniques like Hungarian notation to encode a type in a name is needed in C, but is generally unnecessary and actively harmful in a strongly statically-typed language like C++, because the annotations get out of date (the warts are just like comments and rot just like them) and they interfere with good use of the language (use the same name and overload resolution instead).

##### Note

Some styles use very general (not type-specific) prefixes to denote the general use of a variable.

    auto p = new User();
    auto p = make_unique<User>();
    // note: "p" is not being used to say "raw pointer to type User,"
    //       just generally to say "this is an indirection"

    auto cntHits = calc_total_of_hits(/*...*/);
    // note: "cnt" is not being used to encode a type,
    //       just generally to say "this is a count of something"

This is not harmful and does not fall under this guideline because it does not encode type information.

##### Note

Some styles distinguishes members from local variable, and/or from global variable.

    struct S {
        int m_;
        S(int m) :m_{abs(m)} { }
    };

This is not harmful and does not fall under this guideline because it does not encode type information.

##### Note

Like C++, some styles distinguishes types from non-types.
For example, by capitalizing type names, but not the names of functions and variables.

    typename<typename T>
    class HashTable {   // maps string to T
        // ...
    };

    HashTable<int> index;

This is not harmful and does not fall under this guideline because it does not encode type information.

### <a name="Rl-name-length"></a>NL.7: Make the length of a name roughly proportional to the length of its scope

**Rationale**: The larger the scope the greater the chance of confusion and of an unintended name clash.

##### Example

    double sqrt(double x);   // return the square root of x; x must be non-negative

    int length(const char* p);  // return the number of characters in a zero-terminated C-style string

    int length_of_string(const char zero_terminated_array_of_char[])    // bad: verbose

    int g;      // bad: global variable with a cryptic name

    int open;   // bad: global variable with a short, popular name

The use of `p` for pointer and `x` for a floating-point variable is conventional and non-confusing in a restricted scope.

##### Enforcement

???

### <a name="Rl-name"></a>NL.8: Use a consistent naming style

**Rationale**: Consistence in naming and naming style increases readability.

##### Note

There are many styles and when you use multiple libraries, you can't follow all their different conventions.
Choose a "house style", but leave "imported" libraries with their original style.

##### Example

ISO Standard, use lower case only and digits, separate words with underscores:

* `int`
* `vector`
* `my_map`

Avoid double underscores `__`.

##### Example

[Stroustrup](http://www.stroustrup.com/Programming/PPP-style.pdf):
ISO Standard, but with upper case used for your own types and concepts:

* `int`
* `vector`
* `My_map`

##### Example

CamelCase: capitalize each word in a multi-word identifier:

* `int`
* `vector`
* `MyMap`
* `myMap`

Some conventions capitalize the first letter, some don't.

##### Note

Try to be consistent in your use of acronyms and lengths of identifiers:

    int mtbf {12};
    int mean_time_between_failures {12}; // make up your mind

##### Enforcement

Would be possible except for the use of libraries with varying conventions.

### <a name="Rl-all-caps"></a>NL.9: Use `ALL_CAPS` for macro names only

##### Reason

To avoid confusing macros with names that obey scope and type rules.

##### Example

    void f()
    {
        const int SIZE{1000};  // Bad, use 'size' instead
        int v[SIZE];
    }

##### Note

This rule applies to non-macro symbolic constants:

    enum bad { BAD, WORSE, HORRIBLE }; // BAD

##### Enforcement

* Flag macros with lower-case letters
* Flag `ALL_CAPS` non-macro names

### <a name="Rl-camel"></a>NL.10: Prefer `underscore_style` names

##### Reason

The use of underscores to separate parts of a name is the original C and C++ style and used in the C++ Standard Library.

##### Note

This rule is a default to use only if you have a choice.
Often, you don't have a choice and must follow an established style for [consistency](23_NL_Naming_and_layout_rules.md#Rl-name).
The need for consistency beats personal taste.

##### Example

[Stroustrup](http://www.stroustrup.com/Programming/PPP-style.pdf):
ISO Standard, but with upper case used for your own types and concepts:

* `int`
* `vector`
* `My_map`

##### Enforcement

Impossible.

### <a name="Rl-space"></a>NL.15: Use spaces sparingly

##### Reason

Too much space makes the text larger and distracts.

##### Example, bad

    #include < map >

    int main(int argc, char * argv [ ])
    {
        // ...
    }

##### Example

    #include <map>

    int main(int argc, char* argv[])
    {
        // ...
    }

##### Note

Some IDEs have their own opinions and add distracting space.

##### Note

We value well-placed whitespace as a significant help for readability. Just don't overdo it.

### <a name="Rl-literals"></a>NL.11: Make literals readable

##### Reason

Readability.

##### Example

Use digit separators to avoid long strings of digits

    auto c = 299'792'458; // m/s2
    auto q2 = 0b0000'1111'0000'0000;
    auto ss_number = 123'456'7890;

##### Example

Use literal suffixes where clarification is needed

    auto hello = "Hello!"s; // a std::string
    auto world = "world";   // a C-style string
    auto interval = 100ms;  // using <chrono>

##### Note

Literals should not be sprinkled all over the code as ["magic constants"](09_ES_Expressions_and_statements.md#Res-magic),
but it is still a good idea to make them readable where they are defined.
It is easy to make a typo in a long string of integers.

##### Enforcement

Flag long digit sequences. The trouble is to define "long"; maybe 7.

### <a name="Rl-order"></a>NL.16: Use a conventional class member declaration order

##### Reason

A conventional order of members improves readability.

When declaring a class use the following order

* types: classes, enums, and aliases (`using`)
* constructors, assignments, destructor
* functions
* data

Use the `public` before `protected` before `private` order.

##### Example

    class X {
    public:
        // interface
    protected:
        // unchecked function for use by derived class implementations
    private:
        // implementation details
    };

##### Example

Sometimes, the default order of members conflicts with a desire to separate the public interface from implementation details.
In such cases, private types and functions can be placed with private data.

    class X {
    public:
        // interface
    protected:
        // unchecked function for use by derived class implementations
    private:
        // implementation details (types, functions, and data)
    };

##### Example, bad

Avoid multiple blocks of declarations of one access (e.g., `public`) dispersed among blocks of declarations with different access (e.g. `private`).

    class X {   // bad
    public:
        void f();
    public:
        int g();
        // ...
    };

The use of macros to declare groups of members often leads to violation of any ordering rules.
However, macros obscures what is being expressed anyway.

##### Enforcement

Flag departures from the suggested order. There will be a lot of old code that doesn't follow this rule.

### <a name="Rl-knr"></a>NL.17: Use K&R-derived layout

##### Reason

This is the original C and C++ layout. It preserves vertical space well. It distinguishes different language constructs (such as functions and classes) well.

##### Note

In the context of C++, this style is often called "Stroustrup".

##### Example

    struct Cable {
        int x;
        // ...
    };

    double foo(int x)
    {
        if (0 < x) {
            // ...
        }

        switch (x) {
        case 0:
            // ...
            break;
        case amazing:
            // ...
            break;
        default:
            // ...
            break;
        }

        if (0 < x)
            ++x;

        if (x < 0)
            something();
        else
            something_else();

        return some_value;
    }

Note the space between `if` and `(`

##### Note

Use separate lines for each statement, the branches of an `if`, and the body of a `for`.

##### Note

The `{` for a `class` and a `struct` is *not* on a separate line, but the `{` for a function is.

##### Note

Capitalize the names of your user-defined types to distinguish them from standards-library types.

##### Note

Do not capitalize function names.

##### Enforcement

If you want enforcement, use an IDE to reformat.

### <a name="Rl-ptr"></a>NL.18: Use C++-style declarator layout

##### Reason

The C-style layout emphasizes use in expressions and grammar, whereas the C++-style emphasizes types.
The use in expressions argument doesn't hold for references.

##### Example

    T& operator[](size_t);   // OK
    T &operator[](size_t);   // just strange
    T & operator[](size_t);   // undecided

##### Enforcement

Impossible in the face of history.


### <a name="Rl-misread"></a>NL.19: Avoid names that are easily misread

##### Reason

Readability.
Not everyone has screens and printers that make it easy to distinguish all characters.
We easily confuse similarly spelled and slightly misspelled words.

##### Example

    int oO01lL = 6; // bad

    int splunk = 7;
    int splonk = 8; // bad: splunk and splonk are easily confused

##### Enforcement

???

### <a name="Rl-stmt"></a>NL.20: Don't place two statements on the same line

##### Reason

Readability.
It is really easy to overlook a statement when there is more on a line.

##### Example

    int x = 7; char* p = 29;    // don't
    int x = 7; f(x);  ++x;      // don't

##### Enforcement

Easy.

### <a name="Rl-dcl"></a>NL.21: Declare one name (only) per declaration

##### Reason

Readability.
Minimizing confusion with the declarator syntax.

##### Note

For details, see [ES.10](09_ES_Expressions_and_statements.md#Res-name-one).


### <a name="Rl-void"></a>NL.25: Don't use `void` as an argument type

##### Reason

It's verbose and only needed where C compatibility matters.

##### Example

    void f(void);   // bad

    void g();       // better

##### Note

Even Dennis Ritchie deemed `void f(void)` an abomination.
You can make an argument for that abomination in C when function prototypes were rare so that banning:

    int f();
    f(1, 2, "weird but valid C89");   // hope that f() is defined int f(a, b, c) char* c; { /* ... */ }

would have caused major problems, but not in the 21st century and in C++.

### <a name="Rl-const"></a>NL.26: Use conventional `const` notation

##### Reason

Conventional notation is more familiar to more programmers.
Consistency in large code bases.

##### Example

    const int x = 7;    // OK
    int const y = 9;    // bad

    const int *const p = nullptr;   // OK, constant pointer to constant int
    int const *const p = nullptr;   // bad, constant pointer to constant int

##### Note

We are well aware that you could claim the "bad" examples more logical than the ones marked "OK",
but they also confuse more people, especially novices relying on teaching material using the far more common, conventional OK style.

As ever, remember that the aim of these naming and layout rules is consistency and that aesthetics vary immensely.

##### Enforcement

Flag `const` used as a suffix for a type.

