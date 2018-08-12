# <a name="main"></a>C++ Core Guidelines

April 16, 2018


Editors:

* [Bjarne Stroustrup](http://www.stroustrup.com)
* [Herb Sutter](http://herbsutter.com/)

This is a living document under continuous improvement.
Had it been an open-source (code) project, this would have been release 0.8.
Copying, use, modification, and creation of derivative works from this project is licensed under an MIT-style license.
Contributing to this project requires agreeing to a Contributor License. See the accompanying [LICENSE](LICENSE) file for details.
We make this project available to "friendly users" to use, copy, modify, and derive from, hoping for constructive input.

Comments and suggestions for improvements are most welcome.
We plan to modify and extend this document as our understanding improves and the language and the set of available libraries improve.
When commenting, please note [the introduction](01_main.md#S-introduction) that outlines our aims and general approach.
The list of contributors is [here](20_RF_References.md#SS-ack).

Problems:

* The sets of rules have not been completely checked for completeness, consistency, or enforceability.
* Triple question marks (???) mark known missing information
* Update reference sections; many pre-C++11 sources are too old.
* For a more-or-less up-to-date to-do list see: [To-do: Unclassified proto-rules](01_main.md#S-unclassified)

You can [read an explanation of the scope and structure of this Guide](01_main.md#S-abstract) or just jump straight in:

* [In: Introduction](01_main.md#S-introduction)
* [P: Philosophy](01_main.md#S-philosophy)
* [I: Interfaces](01_main.md#S-interfaces)
* [F: Functions](01_main.md#S-functions)
* [C: Classes and class hierarchies](01_main.md#S-class)
* [Enum: Enumerations](01_main.md#S-enum)
* [R: Resource management](01_main.md#S-resource)
* [ES: Expressions and statements](01_main.md#S-expr)
* [Per: Performance](01_main.md#S-performance)
* [CP: Concurrency and parallelism](01_main.md#S-concurrency)
* [E: Error handling](01_main.md#S-errors)
* [Con: Constants and immutability](01_main.md#S-const)
* [T: Templates and generic programming](01_main.md#S-templates)
* [CPL: C-style programming](01_main.md#S-cpl)
* [SF: Source files](01_main.md#S-source)
* [SL: The Standard Library](01_main.md#S-stdlib)

Supporting sections:

* [A: Architectural ideas](01_main.md#S-A)
* [NR: Non-Rules and myths](01_main.md#S-not)
* [RF: References](01_main.md#S-references)
* [Pro: Profiles](01_main.md#S-profile)
* [GSL: Guidelines support library](01_main.md#S-gsl)
* [NL: Naming and layout rules](01_main.md#S-naming)
* [FAQ: Answers to frequently asked questions](01_main.md#S-faq)
* [Appendix A: Libraries](01_main.md#S-libraries)
* [Appendix B: Modernizing code](01_main.md#S-modernizing)
* [Appendix C: Discussion](01_main.md#S-discussion)
* [Appendix D: Supporting tools](01_main.md#S-tools)
* [Glossary](01_main.md#S-glossary)
* [To-do: Unclassified proto-rules](01_main.md#S-unclassified)

You can sample rules for specific language features:

* assignment:
[regular types](06_C_Classes_and_class_hierarchies.md#Rc-regular) --
[prefer initialization](06_C_Classes_and_class_hierarchies.md#Rc-initialize) --
[copy](06_C_Classes_and_class_hierarchies.md#Rc-copy-semantic) --
[move](06_C_Classes_and_class_hierarchies.md#Rc-move-semantic) --
[other operations](06_C_Classes_and_class_hierarchies.md#Rc-matched) --
[default](06_C_Classes_and_class_hierarchies.md#Rc-eqdefault)
* `class`:
[data](06_C_Classes_and_class_hierarchies.md#Rc-org) --
[invariant](06_C_Classes_and_class_hierarchies.md#Rc-struct) --
[members](06_C_Classes_and_class_hierarchies.md#Rc-member) --
[helpers](06_C_Classes_and_class_hierarchies.md#Rc-helper) --
[concrete types](06_C_Classes_and_class_hierarchies.md#SS-concrete) --
[ctors, =, and dtors](06_C_Classes_and_class_hierarchies.md#S-ctor) --
[hierarchy](06_C_Classes_and_class_hierarchies.md#SS-hier) --
[operators](06_C_Classes_and_class_hierarchies.md#SS-overload)
* `concept`:
[rules](14_T_Templates_and_generic_programming.md#SS-concepts) --
[in generic programming](14_T_Templates_and_generic_programming.md#Rt-raise) --
[template arguments](14_T_Templates_and_generic_programming.md#Rt-concepts) --
[semantics](14_T_Templates_and_generic_programming.md#Rt-low)
* constructor:
[invariant](06_C_Classes_and_class_hierarchies.md#Rc-struct) --
[establish invariant](06_C_Classes_and_class_hierarchies.md#Rc-ctor) --
[`throw`](06_C_Classes_and_class_hierarchies.md#Rc-throw) --
[default](06_C_Classes_and_class_hierarchies.md#Rc-default0) --
[not needed](06_C_Classes_and_class_hierarchies.md#Rc-default) --
[`explicit`](06_C_Classes_and_class_hierarchies.md#Rc-explicit) --
[delegating](06_C_Classes_and_class_hierarchies.md#Rc-delegating) --
[`virtual`](06_C_Classes_and_class_hierarchies.md#Rc-ctor-virtual)
* derived `class`:
[when to use](06_C_Classes_and_class_hierarchies.md#Rh-domain) --
[as interface](06_C_Classes_and_class_hierarchies.md#Rh-abstract) --
[destructors](06_C_Classes_and_class_hierarchies.md#Rh-dtor) --
[copy](06_C_Classes_and_class_hierarchies.md#Rh-copy) --
[getters and setters](06_C_Classes_and_class_hierarchies.md#Rh-get) --
[multiple inheritance](06_C_Classes_and_class_hierarchies.md#Rh-mi-interface) --
[overloading](06_C_Classes_and_class_hierarchies.md#Rh-using) --
[slicing](06_C_Classes_and_class_hierarchies.md#Rc-copy-virtual) --
[`dynamic_cast`](06_C_Classes_and_class_hierarchies.md#Rh-dynamic_cast)
* destructor:
[and constructors](06_C_Classes_and_class_hierarchies.md#Rc-matched) --
[when needed?](06_C_Classes_and_class_hierarchies.md#Rc-dtor) --
[may not fail](06_C_Classes_and_class_hierarchies.md#Rc-dtor-fail)
* exception:
[errors](01_main.md#S-errors) --
[`throw`](12_E_Error_handling.md#Re-throw) --
[for errors only](12_E_Error_handling.md#Re-errors) --
[`noexcept`](12_E_Error_handling.md#Re-noexcept) --
[minimize `try`](12_E_Error_handling.md#Re-catch) --
[what if no exceptions?](12_E_Error_handling.md#Re-no-throw-codes)
* `for`:
[range-for and for](09_ES_Expressions_and_statements.md#Res-for-range) --
[for and while](09_ES_Expressions_and_statements.md#Res-for-while) --
[for-initializer](09_ES_Expressions_and_statements.md#Res-for-init) --
[empty body](09_ES_Expressions_and_statements.md#Res-empty) --
[loop variable](09_ES_Expressions_and_statements.md#Res-loop-counter) --
[loop variable type ???](#Res-???)
* function:
[naming](05_F_Functions.md#Rf-package) --
[single operation](05_F_Functions.md#Rf-logical) --
[no throw](05_F_Functions.md#Rf-noexcept) --
[arguments](05_F_Functions.md#Rf-smart) --
[argument passing](05_F_Functions.md#Rf-conventional) --
[multiple return values](05_F_Functions.md#Rf-out-multi) --
[pointers](05_F_Functions.md#Rf-return-ptr) --
[lambdas](05_F_Functions.md#Rf-capture-vs-overload)
* `inline`:
[small functions](05_F_Functions.md#Rf-inline) --
[in headers](16_SF_Source_files.md#Rs-inline)
* initialization:
[always](09_ES_Expressions_and_statements.md#Res-always) --
[prefer `{}`](09_ES_Expressions_and_statements.md#Res-list) --
[lambdas](09_ES_Expressions_and_statements.md#Res-lambda-init) --
[in-class initializers](06_C_Classes_and_class_hierarchies.md#Rc-in-class-initializer) --
[class members](06_C_Classes_and_class_hierarchies.md#Rc-initialize) --
[factory functions](06_C_Classes_and_class_hierarchies.md#Rc-factory)
* lambda expression:
[when to use](06_C_Classes_and_class_hierarchies.md#SS-lambdas)
* operator:
[conventional](06_C_Classes_and_class_hierarchies.md#Ro-conventional) --
[avoid conversion operators](06_C_Classes_and_class_hierarchies.md#Ro-conversion) --
[and lambdas](06_C_Classes_and_class_hierarchies.md#Ro-lambda)
* `public`, `private`, and `protected`:
[information hiding](06_C_Classes_and_class_hierarchies.md#Rc-private) --
[consistency](06_C_Classes_and_class_hierarchies.md#Rh-public) --
[`protected`](06_C_Classes_and_class_hierarchies.md#Rh-protected)
* `static_assert`:
[compile-time checking](03_P_Philosophy.md#Rp-compile-time) --
[and concepts](14_T_Templates_and_generic_programming.md#Rt-check-class)
* `struct`:
[for organizing data](06_C_Classes_and_class_hierarchies.md#Rc-org) --
[use if no invariant](06_C_Classes_and_class_hierarchies.md#Rc-struct) --
[no private members](06_C_Classes_and_class_hierarchies.md#Rc-class)
* `template`:
[abstraction](14_T_Templates_and_generic_programming.md#Rt-raise) --
[containers](14_T_Templates_and_generic_programming.md#Rt-cont) --
[concepts](14_T_Templates_and_generic_programming.md#Rt-concepts)
* `unsigned`:
[and signed](09_ES_Expressions_and_statements.md#Res-mix) --
[bit manipulation](09_ES_Expressions_and_statements.md#Res-unsigned)
* `virtual`:
[interfaces](04_I_Interfaces.md#Ri-abstract) --
[not `virtual`](06_C_Classes_and_class_hierarchies.md#Rc-concrete) --
[destructor](06_C_Classes_and_class_hierarchies.md#Rc-dtor-virtual) --
[never fail](06_C_Classes_and_class_hierarchies.md#Rc-dtor-fail)

You can look at design concepts used to express the rules:

* assertion: ???
* error: ???
* exception: exception guarantee (???)
* failure: ???
* invariant: ???
* leak: ???
* library: ???
* precondition: ???
* postcondition: ???
* resource: ???

# <a name="S-abstract"></a>Abstract

This document is a set of guidelines for using C++ well.
The aim of this document is to help people to use modern C++ effectively.
By "modern C++" we mean C++17, C++14, and C++11.
In other words, what would you like your code to look like in 5 years' time, given that you can start now? In 10 years' time?

The guidelines are focused on relatively high-level issues, such as interfaces, resource management, memory management, and concurrency.
Such rules affect application architecture and library design.
Following the rules will lead to code that is statically type safe, has no resource leaks, and catches many more programming logic errors than is common in code today.
And it will run fast -- you can afford to do things right.

We are less concerned with low-level issues, such as naming conventions and indentation style.
However, no topic that can help a programmer is out of bounds.

Our initial set of rules emphasizes safety (of various forms) and simplicity.
They may very well be too strict.
We expect to have to introduce more exceptions to better accommodate real-world needs.
We also need more rules.

You will find some of the rules contrary to your expectations or even contrary to your experience.
If we haven't suggested you change your coding style in any way, we have failed!
Please try to verify or disprove rules!
In particular, we'd really like to have some of our rules backed up with measurements or better examples.

You will find some of the rules obvious or even trivial.
Please remember that one purpose of a guideline is to help someone who is less experienced or coming from a different background or language to get up to speed.

Many of the rules are designed to be supported by an analysis tool.
Violations of rules will be flagged with references (or links) to the relevant rule.
We do not expect you to memorize all the rules before trying to write code.
One way of thinking about these guidelines is as a specification for tools that happens to be readable by humans.

The rules are meant for gradual introduction into a code base.
We plan to build tools for that and hope others will too.

Comments and suggestions for improvements are most welcome.
We plan to modify and extend this document as our understanding improves and the language and the set of available libraries improve.

# <a name="S-introduction"></a>In: Introduction

This is a set of core guidelines for modern C++, C++17, C++14, and C++11, taking likely future enhancements and ISO Technical Specifications (TSs) into account.
The aim is to help C++ programmers to write simpler, more efficient, more maintainable code.

Introduction summary:

* [In.target: Target readership](02_In_Introduction.md#SS-readers)
* [In.aims: Aims](02_In_Introduction.md#SS-aims)
* [In.not: Non-aims](02_In_Introduction.md#SS-non)
* [In.force: Enforcement](02_In_Introduction.md#SS-force)
* [In.struct: The structure of this document](02_In_Introduction.md#SS-struct)
* [In.sec: Major sections](02_In_Introduction.md#SS-sec)

# <a name="S-philosophy"></a>P: Philosophy

The rules in this section are very general.

Philosophy rules summary:

* [P.1: Express ideas directly in code](03_P_Philosophy.md#Rp-direct)
* [P.2: Write in ISO Standard C++](03_P_Philosophy.md#Rp-Cplusplus)
* [P.3: Express intent](03_P_Philosophy.md#Rp-what)
* [P.4: Ideally, a program should be statically type safe](03_P_Philosophy.md#Rp-typesafe)
* [P.5: Prefer compile-time checking to run-time checking](03_P_Philosophy.md#Rp-compile-time)
* [P.6: What cannot be checked at compile time should be checkable at run time](03_P_Philosophy.md#Rp-run-time)
* [P.7: Catch run-time errors early](03_P_Philosophy.md#Rp-early)
* [P.8: Don't leak any resources](03_P_Philosophy.md#Rp-leak)
* [P.9: Don't waste time or space](03_P_Philosophy.md#Rp-waste)
* [P.10: Prefer immutable data to mutable data](03_P_Philosophy.md#Rp-mutable)
* [P.11: Encapsulate messy constructs, rather than spreading through the code](03_P_Philosophy.md#Rp-library)
* [P.12: Use supporting tools as appropriate](03_P_Philosophy.md#Rp-tools)
* [P.13: Use support libraries as appropriate](03_P_Philosophy.md#Rp-lib)

Philosophical rules are generally not mechanically checkable.
However, individual rules reflecting these philosophical themes are.
Without a philosophical basis, the more concrete/specific/checkable rules lack rationale.

# <a name="S-interfaces"></a>I: Interfaces

An interface is a contract between two parts of a program. Precisely stating what is expected of a supplier of a service and a user of that service is essential.
Having good (easy-to-understand, encouraging efficient use, not error-prone, supporting testing, etc.) interfaces is probably the most important single aspect of code organization.

Interface rule summary:

* [I.1: Make interfaces explicit](04_I_Interfaces.md#Ri-explicit)
* [I.2: Avoid non-`const` global variables](04_I_Interfaces.md#Ri-global)
* [I.3: Avoid singletons](04_I_Interfaces.md#Ri-singleton)
* [I.4: Make interfaces precisely and strongly typed](04_I_Interfaces.md#Ri-typed)
* [I.5: State preconditions (if any)](04_I_Interfaces.md#Ri-pre)
* [I.6: Prefer `Expects()` for expressing preconditions](04_I_Interfaces.md#Ri-expects)
* [I.7: State postconditions](04_I_Interfaces.md#Ri-post)
* [I.8: Prefer `Ensures()` for expressing postconditions](04_I_Interfaces.md#Ri-ensures)
* [I.9: If an interface is a template, document its parameters using concepts](04_I_Interfaces.md#Ri-concepts)
* [I.10: Use exceptions to signal a failure to perform a required task](04_I_Interfaces.md#Ri-except)
* [I.11: Never transfer ownership by a raw pointer (`T*`) or reference (`T&`)](04_I_Interfaces.md#Ri-raw)
* [I.12: Declare a pointer that must not be null as `not_null`](04_I_Interfaces.md#Ri-nullptr)
* [I.13: Do not pass an array as a single pointer](04_I_Interfaces.md#Ri-array)
* [I.22: Avoid complex initialization of global objects](04_I_Interfaces.md#Ri-global-init)
* [I.23: Keep the number of function arguments low](04_I_Interfaces.md#Ri-nargs)
* [I.24: Avoid adjacent unrelated parameters of the same type](04_I_Interfaces.md#Ri-unrelated)
* [I.25: Prefer abstract classes as interfaces to class hierarchies](04_I_Interfaces.md#Ri-abstract)
* [I.26: If you want a cross-compiler ABI, use a C-style subset](04_I_Interfaces.md#Ri-abi)
* [I.27: For stable library ABI, consider the Pimpl idiom](04_I_Interfaces.md#Ri-pimpl)
* [I.30: Encapsulate rule violations](04_I_Interfaces.md#Ri-encapsulate)

**See also**:

* [F: Functions](01_main.md#S-functions)
* [C.concrete: Concrete types](06_C_Classes_and_class_hierarchies.md#SS-concrete)
* [C.hier: Class hierarchies](06_C_Classes_and_class_hierarchies.md#SS-hier)
* [C.over: Overloading and overloaded operators](06_C_Classes_and_class_hierarchies.md#SS-overload)
* [C.con: Containers and other resource handles](06_C_Classes_and_class_hierarchies.md#SS-containers)
* [E: Error handling](01_main.md#S-errors)
* [T: Templates and generic programming](01_main.md#S-templates)

# <a name="S-functions"></a>F: Functions

A function specifies an action or a computation that takes the system from one consistent state to the next. It is the fundamental building block of programs.

It should be possible to name a function meaningfully, to specify the requirements of its argument, and clearly state the relationship between the arguments and the result. An implementation is not a specification. Try to think about what a function does as well as about how it does it.
Functions are the most critical part in most interfaces, so see the interface rules.

Function rule summary:

Function definition rules:

* [F.1: "Package" meaningful operations as carefully named functions](05_F_Functions.md#Rf-package)
* [F.2: A function should perform a single logical operation](05_F_Functions.md#Rf-logical)
* [F.3: Keep functions short and simple](05_F_Functions.md#Rf-single)
* [F.4: If a function may have to be evaluated at compile time, declare it `constexpr`](05_F_Functions.md#Rf-constexpr)
* [F.5: If a function is very small and time-critical, declare it inline](05_F_Functions.md#Rf-inline)
* [F.6: If your function may not throw, declare it `noexcept`](05_F_Functions.md#Rf-noexcept)
* [F.7: For general use, take `T*` or `T&` arguments rather than smart pointers](05_F_Functions.md#Rf-smart)
* [F.8: Prefer pure functions](05_F_Functions.md#Rf-pure)
* [F.9: Unused parameters should be unnamed](05_F_Functions.md#Rf-unused)

Parameter passing expression rules:

* [F.15: Prefer simple and conventional ways of passing information](05_F_Functions.md#Rf-conventional)
* [F.16: For "in" parameters, pass cheaply-copied types by value and others by reference to `const`](05_F_Functions.md#Rf-in)
* [F.17: For "in-out" parameters, pass by reference to non-`const`](05_F_Functions.md#Rf-inout)
* [F.18: For "will-move-from" parameters, pass by `X&&` and `std::move` the parameter](05_F_Functions.md#Rf-consume)
* [F.19: For "forward" parameters, pass by `TP&&` and only `std::forward` the parameter](05_F_Functions.md#Rf-forward)
* [F.20: For "out" output values, prefer return values to output parameters](05_F_Functions.md#Rf-out)
* [F.21: To return multiple "out" values, prefer returning a struct or tuple](05_F_Functions.md#Rf-out-multi)
* [F.60: Prefer `T*` over `T&` when "no argument" is a valid option](05_F_Functions.md#Rf-ptr-ref)

Parameter passing semantic rules:

* [F.22: Use `T*` or `owner<T*>` to designate a single object](05_F_Functions.md#Rf-ptr)
* [F.23: Use a `not_null<T>` to indicate that "null" is not a valid value](05_F_Functions.md#Rf-nullptr)
* [F.24: Use a `span<T>` or a `span_p<T>` to designate a half-open sequence](05_F_Functions.md#Rf-range)
* [F.25: Use a `zstring` or a `not_null<zstring>` to designate a C-style string](05_F_Functions.md#Rf-zstring)
* [F.26: Use a `unique_ptr<T>` to transfer ownership where a pointer is needed](05_F_Functions.md#Rf-unique_ptr)
* [F.27: Use a `shared_ptr<T>` to share ownership](05_F_Functions.md#Rf-shared_ptr)

<a name="Rf-value-return"></a>Value return semantic rules:

* [F.42: Return a `T*` to indicate a position (only)](05_F_Functions.md#Rf-return-ptr)
* [F.43: Never (directly or indirectly) return a pointer or a reference to a local object](05_F_Functions.md#Rf-dangle)
* [F.44: Return a `T&` when copy is undesirable and "returning no object" isn't needed](05_F_Functions.md#Rf-return-ref)
* [F.45: Don't return a `T&&`](05_F_Functions.md#Rf-return-ref-ref)
* [F.46: `int` is the return type for `main()`](05_F_Functions.md#Rf-main)
* [F.47: Return `T&` from assignment operators](05_F_Functions.md#Rf-assignment-op)
* [F.48: Don't `return std::move(local)`](05_F_Functions.md#Rf-return-move-local)

Other function rules:

* [F.50: Use a lambda when a function won't do (to capture local variables, or to write a local function)](05_F_Functions.md#Rf-capture-vs-overload)
* [F.51: Where there is a choice, prefer default arguments over overloading](05_F_Functions.md#Rf-default-args)
* [F.52: Prefer capturing by reference in lambdas that will be used locally, including passed to algorithms](05_F_Functions.md#Rf-reference-capture)
* [F.53: Avoid capturing by reference in lambdas that will be used nonlocally, including returned, stored on the heap, or passed to another thread](05_F_Functions.md#Rf-value-capture)
* [F.54: If you capture `this`, capture all variables explicitly (no default capture)](05_F_Functions.md#Rf-this-capture)
* [F.55: Don't use `va_arg` arguments](05_F_Functions.md#F-varargs)

Functions have strong similarities to lambdas and function objects.

**See also**: [C.lambdas: Function objects and lambdas](06_C_Classes_and_class_hierarchies.md#SS-lambdas)

# <a name="S-class"></a>C: Classes and class hierarchies

A class is a user-defined type, for which a programmer can define the representation, operations, and interfaces.
Class hierarchies are used to organize related classes into hierarchical structures.

Class rule summary:

* [C.1: Organize related data into structures (`struct`s or `class`es)](06_C_Classes_and_class_hierarchies.md#Rc-org)
* [C.2: Use `class` if the class has an invariant; use `struct` if the data members can vary independently](06_C_Classes_and_class_hierarchies.md#Rc-struct)
* [C.3: Represent the distinction between an interface and an implementation using a class](06_C_Classes_and_class_hierarchies.md#Rc-interface)
* [C.4: Make a function a member only if it needs direct access to the representation of a class](06_C_Classes_and_class_hierarchies.md#Rc-member)
* [C.5: Place helper functions in the same namespace as the class they support](06_C_Classes_and_class_hierarchies.md#Rc-helper)
* [C.7: Don't define a class or enum and declare a variable of its type in the same statement](06_C_Classes_and_class_hierarchies.md#Rc-standalone)
* [C.8: Use `class` rather than `struct` if any member is non-public](06_C_Classes_and_class_hierarchies.md#Rc-class)
* [C.9: Minimize exposure of members](06_C_Classes_and_class_hierarchies.md#Rc-private)

Subsections:

* [C.concrete: Concrete types](06_C_Classes_and_class_hierarchies.md#SS-concrete)
* [C.ctor: Constructors, assignments, and destructors](06_C_Classes_and_class_hierarchies.md#S-ctor)
* [C.con: Containers and other resource handles](06_C_Classes_and_class_hierarchies.md#SS-containers)
* [C.lambdas: Function objects and lambdas](06_C_Classes_and_class_hierarchies.md#SS-lambdas)
* [C.hier: Class hierarchies (OOP)](06_C_Classes_and_class_hierarchies.md#SS-hier)
* [C.over: Overloading and overloaded operators](06_C_Classes_and_class_hierarchies.md#SS-overload)
* [C.union: Unions](06_C_Classes_and_class_hierarchies.md#SS-union)

# <a name="S-enum"></a>Enum: Enumerations

Enumerations are used to define sets of integer values and for defining types for such sets of values.
There are two kind of enumerations, "plain" `enum`s and `class enum`s.

Enumeration rule summary:

* [Enum.1: Prefer enumerations over macros](07_Enum_Enumerations.md#Renum-macro)
* [Enum.2: Use enumerations to represent sets of related named constants](07_Enum_Enumerations.md#Renum-set)
* [Enum.3: Prefer `enum class`es over "plain" `enum`s](07_Enum_Enumerations.md#Renum-class)
* [Enum.4: Define operations on enumerations for safe and simple use](07_Enum_Enumerations.md#Renum-oper)
* [Enum.5: Don't use `ALL_CAPS` for enumerators](07_Enum_Enumerations.md#Renum-caps)
* [Enum.6: Avoid unnamed enumerations](07_Enum_Enumerations.md#Renum-unnamed)
* [Enum.7: Specify the underlying type of an enumeration only when necessary](07_Enum_Enumerations.md#Renum-underlying)
* [Enum.8: Specify enumerator values only when necessary](07_Enum_Enumerations.md#Renum-value)

# <a name="S-resource"></a>R: Resource management

This section contains rules related to resources.
A resource is anything that must be acquired and (explicitly or implicitly) released, such as memory, file handles, sockets, and locks.
The reason it must be released is typically that it can be in short supply, so even delayed release may do harm.
The fundamental aim is to ensure that we don't leak any resources and that we don't hold a resource longer than we need to.
An entity that is responsible for releasing a resource is called an owner.

There are a few cases where leaks can be acceptable or even optimal:
If you are writing a program that simply produces an output based on an input and the amount of memory needed is proportional to the size of the input, the optimal strategy (for performance and ease of programming) is sometimes simply never to delete anything.
If you have enough memory to handle your largest input, leak away, but be sure to give a good error message if you are wrong.
Here, we ignore such cases.

* Resource management rule summary:

  * [R.1: Manage resources automatically using resource handles and RAII (Resource Acquisition Is Initialization)](08_R_Resource_management.md#Rr-raii)
  * [R.2: In interfaces, use raw pointers to denote individual objects (only)](08_R_Resource_management.md#Rr-use-ptr)
  * [R.3: A raw pointer (a `T*`) is non-owning](08_R_Resource_management.md#Rr-ptr)
  * [R.4: A raw reference (a `T&`) is non-owning](08_R_Resource_management.md#Rr-ref)
  * [R.5: Prefer scoped objects, don't heap-allocate unnecessarily](08_R_Resource_management.md#Rr-scoped)
  * [R.6: Avoid non-`const` global variables](08_R_Resource_management.md#Rr-global)

* Allocation and deallocation rule summary:

  * [R.10: Avoid `malloc()` and `free()`](08_R_Resource_management.md#Rr-mallocfree)
  * [R.11: Avoid calling `new` and `delete` explicitly](08_R_Resource_management.md#Rr-newdelete)
  * [R.12: Immediately give the result of an explicit resource allocation to a manager object](08_R_Resource_management.md#Rr-immediate-alloc)
  * [R.13: Perform at most one explicit resource allocation in a single expression statement](08_R_Resource_management.md#Rr-single-alloc)
  * [R.14: ??? array vs. pointer parameter](08_R_Resource_management.md#Rr-ap)
  * [R.15: Always overload matched allocation/deallocation pairs](08_R_Resource_management.md#Rr-pair)

* <a name="Rr-summary-smartptrs"></a>Smart pointer rule summary:

  * [R.20: Use `unique_ptr` or `shared_ptr` to represent ownership](08_R_Resource_management.md#Rr-owner)
  * [R.21: Prefer `unique_ptr` over `shared_ptr` unless you need to share ownership](08_R_Resource_management.md#Rr-unique)
  * [R.22: Use `make_shared()` to make `shared_ptr`s](08_R_Resource_management.md#Rr-make_shared)
  * [R.23: Use `make_unique()` to make `unique_ptr`s](08_R_Resource_management.md#Rr-make_unique)
  * [R.24: Use `std::weak_ptr` to break cycles of `shared_ptr`s](08_R_Resource_management.md#Rr-weak_ptr)
  * [R.30: Take smart pointers as parameters only to explicitly express lifetime semantics](08_R_Resource_management.md#Rr-smartptrparam)
  * [R.31: If you have non-`std` smart pointers, follow the basic pattern from `std`](08_R_Resource_management.md#Rr-smart)
  * [R.32: Take a `unique_ptr<widget>` parameter to express that a function assumes ownership of a `widget`](08_R_Resource_management.md#Rr-uniqueptrparam)
  * [R.33: Take a `unique_ptr<widget>&` parameter to express that a function reseats the `widget`](08_R_Resource_management.md#Rr-reseat)
  * [R.34: Take a `shared_ptr<widget>` parameter to express that a function is part owner](08_R_Resource_management.md#Rr-sharedptrparam-owner)
  * [R.35: Take a `shared_ptr<widget>&` parameter to express that a function might reseat the shared pointer](08_R_Resource_management.md#Rr-sharedptrparam)
  * [R.36: Take a `const shared_ptr<widget>&` parameter to express that it might retain a reference count to the object ???](08_R_Resource_management.md#Rr-sharedptrparam-const)
  * [R.37: Do not pass a pointer or reference obtained from an aliased smart pointer](08_R_Resource_management.md#Rr-smartptrget)

# <a name="S-expr"></a>ES: Expressions and statements

Expressions and statements are the lowest and most direct way of expressing actions and computation. Declarations in local scopes are statements.

For naming, commenting, and indentation rules, see [NL: Naming and layout](01_main.md#S-naming).

General rules:

* [ES.1: Prefer the standard library to other libraries and to "handcrafted code"](09_ES_Expressions_and_statements.md#Res-lib)
* [ES.2: Prefer suitable abstractions to direct use of language features](09_ES_Expressions_and_statements.md#Res-abstr)

Declaration rules:

* [ES.5: Keep scopes small](09_ES_Expressions_and_statements.md#Res-scope)
* [ES.6: Declare names in for-statement initializers and conditions to limit scope](09_ES_Expressions_and_statements.md#Res-cond)
* [ES.7: Keep common and local names short, and keep uncommon and nonlocal names longer](09_ES_Expressions_and_statements.md#Res-name-length)
* [ES.8: Avoid similar-looking names](09_ES_Expressions_and_statements.md#Res-name-similar)
* [ES.9: Avoid `ALL_CAPS` names](09_ES_Expressions_and_statements.md#Res-not-CAPS)
* [ES.10: Declare one name (only) per declaration](09_ES_Expressions_and_statements.md#Res-name-one)
* [ES.11: Use `auto` to avoid redundant repetition of type names](09_ES_Expressions_and_statements.md#Res-auto)
* [ES.12: Do not reuse names in nested scopes](09_ES_Expressions_and_statements.md#Res-reuse)
* [ES.20: Always initialize an object](09_ES_Expressions_and_statements.md#Res-always)
* [ES.21: Don't introduce a variable (or constant) before you need to use it](09_ES_Expressions_and_statements.md#Res-introduce)
* [ES.22: Don't declare a variable until you have a value to initialize it with](09_ES_Expressions_and_statements.md#Res-init)
* [ES.23: Prefer the `{}`-initializer syntax](09_ES_Expressions_and_statements.md#Res-list)
* [ES.24: Use a `unique_ptr<T>` to hold pointers](09_ES_Expressions_and_statements.md#Res-unique)
* [ES.25: Declare an object `const` or `constexpr` unless you want to modify its value later on](09_ES_Expressions_and_statements.md#Res-const)
* [ES.26: Don't use a variable for two unrelated purposes](09_ES_Expressions_and_statements.md#Res-recycle)
* [ES.27: Use `std::array` or `stack_array` for arrays on the stack](09_ES_Expressions_and_statements.md#Res-stack)
* [ES.28: Use lambdas for complex initialization, especially of `const` variables](09_ES_Expressions_and_statements.md#Res-lambda-init)
* [ES.30: Don't use macros for program text manipulation](09_ES_Expressions_and_statements.md#Res-macros)
* [ES.31: Don't use macros for constants or "functions"](09_ES_Expressions_and_statements.md#Res-macros2)
* [ES.32: Use `ALL_CAPS` for all macro names](09_ES_Expressions_and_statements.md#Res-ALL_CAPS)
* [ES.33: If you must use macros, give them unique names](09_ES_Expressions_and_statements.md#Res-MACROS)
* [ES.34: Don't define a (C-style) variadic function](09_ES_Expressions_and_statements.md#Res-ellipses)

Expression rules:

* [ES.40: Avoid complicated expressions](09_ES_Expressions_and_statements.md#Res-complicated)
* [ES.41: If in doubt about operator precedence, parenthesize](09_ES_Expressions_and_statements.md#Res-parens)
* [ES.42: Keep use of pointers simple and straightforward](09_ES_Expressions_and_statements.md#Res-ptr)
* [ES.43: Avoid expressions with undefined order of evaluation](09_ES_Expressions_and_statements.md#Res-order)
* [ES.44: Don't depend on order of evaluation of function arguments](09_ES_Expressions_and_statements.md#Res-order-fct)
* [ES.45: Avoid "magic constants"; use symbolic constants](09_ES_Expressions_and_statements.md#Res-magic)
* [ES.46: Avoid narrowing conversions](09_ES_Expressions_and_statements.md#Res-narrowing)
* [ES.47: Use `nullptr` rather than `0` or `NULL`](09_ES_Expressions_and_statements.md#Res-nullptr)
* [ES.48: Avoid casts](09_ES_Expressions_and_statements.md#Res-casts)
* [ES.49: If you must use a cast, use a named cast](09_ES_Expressions_and_statements.md#Res-casts-named)
* [ES.50: Don't cast away `const`](09_ES_Expressions_and_statements.md#Res-casts-const)
* [ES.55: Avoid the need for range checking](09_ES_Expressions_and_statements.md#Res-range-checking)
* [ES.56: Write `std::move()` only when you need to explicitly move an object to another scope](09_ES_Expressions_and_statements.md#Res-move)
* [ES.60: Avoid `new` and `delete` outside resource management functions](09_ES_Expressions_and_statements.md#Res-new)
* [ES.61: Delete arrays using `delete[]` and non-arrays using `delete`](09_ES_Expressions_and_statements.md#Res-del)
* [ES.62: Don't compare pointers into different arrays](09_ES_Expressions_and_statements.md#Res-arr2)
* [ES.63: Don't slice](09_ES_Expressions_and_statements.md#Res-slice)
* [ES.64: Use the `T{e}`notation for construction](09_ES_Expressions_and_statements.md#Res-construct)
* [ES.65: Don't dereference an invalid pointer](09_ES_Expressions_and_statements.md#Res-deref)

Statement rules:

* [ES.70: Prefer a `switch`-statement to an `if`-statement when there is a choice](09_ES_Expressions_and_statements.md#Res-switch-if)
* [ES.71: Prefer a range-`for`-statement to a `for`-statement when there is a choice](09_ES_Expressions_and_statements.md#Res-for-range)
* [ES.72: Prefer a `for`-statement to a `while`-statement when there is an obvious loop variable](09_ES_Expressions_and_statements.md#Res-for-while)
* [ES.73: Prefer a `while`-statement to a `for`-statement when there is no obvious loop variable](09_ES_Expressions_and_statements.md#Res-while-for)
* [ES.74: Prefer to declare a loop variable in the initializer part of a `for`-statement](09_ES_Expressions_and_statements.md#Res-for-init)
* [ES.75: Avoid `do`-statements](09_ES_Expressions_and_statements.md#Res-do)
* [ES.76: Avoid `goto`](09_ES_Expressions_and_statements.md#Res-goto)
* [ES.77: Minimize the use of `break` and `continue` in loops](09_ES_Expressions_and_statements.md#Res-continue)
* [ES.78: Always end a non-empty `case` with a `break`](09_ES_Expressions_and_statements.md#Res-break)
* [ES.79: Use `default` to handle common cases (only)](09_ES_Expressions_and_statements.md#Res-default)
* [ES.84: Don't (try to) declare a local variable with no name](09_ES_Expressions_and_statements.md#Res-noname)
* [ES.85: Make empty statements visible](09_ES_Expressions_and_statements.md#Res-empty)
* [ES.86: Avoid modifying loop control variables inside the body of raw for-loops](09_ES_Expressions_and_statements.md#Res-loop-counter)
* [ES.87: Don't add redundant `==` or `!=` to conditions](09_ES_Expressions_and_statements.md#Res-if)

Arithmetic rules:

* [ES.100: Don't mix signed and unsigned arithmetic](09_ES_Expressions_and_statements.md#Res-mix)
* [ES.101: Use unsigned types for bit manipulation](09_ES_Expressions_and_statements.md#Res-unsigned)
* [ES.102: Use signed types for arithmetic](09_ES_Expressions_and_statements.md#Res-signed)
* [ES.103: Don't overflow](09_ES_Expressions_and_statements.md#Res-overflow)
* [ES.104: Don't underflow](09_ES_Expressions_and_statements.md#Res-underflow)
* [ES.105: Don't divide by zero](09_ES_Expressions_and_statements.md#Res-zero)
* [ES.106: Don't try to avoid negative values by using `unsigned`](09_ES_Expressions_and_statements.md#Res-nonnegative)
* [ES.107: Don't use `unsigned` for subscripts, prefer `gsl::index`](09_ES_Expressions_and_statements.md#Res-subscripts)

# <a name="S-performance"></a>Per: Performance

??? should this section be in the main guide???

This section contains rules for people who need high performance or low-latency.
That is, these are rules that relate to how to use as little time and as few resources as possible to achieve a task in a predictably short time.
The rules in this section are more restrictive and intrusive than what is needed for many (most) applications.
Do not blindly try to follow them in general code: achieving the goals of low latency requires extra work.

Performance rule summary:

* [Per.1: Don't optimize without reason](10_Per_Performance.md#Rper-reason)
* [Per.2: Don't optimize prematurely](10_Per_Performance.md#Rper-Knuth)
* [Per.3: Don't optimize something that's not performance critical](10_Per_Performance.md#Rper-critical)
* [Per.4: Don't assume that complicated code is necessarily faster than simple code](10_Per_Performance.md#Rper-simple)
* [Per.5: Don't assume that low-level code is necessarily faster than high-level code](10_Per_Performance.md#Rper-low)
* [Per.6: Don't make claims about performance without measurements](10_Per_Performance.md#Rper-measure)
* [Per.7: Design to enable optimization](10_Per_Performance.md#Rper-efficiency)
* [Per.10: Rely on the static type system](10_Per_Performance.md#Rper-type)
* [Per.11: Move computation from run time to compile time](10_Per_Performance.md#Rper-Comp)
* [Per.12: Eliminate redundant aliases](10_Per_Performance.md#Rper-alias)
* [Per.13: Eliminate redundant indirections](10_Per_Performance.md#Rper-indirect)
* [Per.14: Minimize the number of allocations and deallocations](10_Per_Performance.md#Rper-alloc)
* [Per.15: Do not allocate on a critical branch](10_Per_Performance.md#Rper-alloc0)
* [Per.16: Use compact data structures](10_Per_Performance.md#Rper-compact)
* [Per.17: Declare the most used member of a time-critical struct first](10_Per_Performance.md#Rper-struct)
* [Per.18: Space is time](10_Per_Performance.md#Rper-space)
* [Per.19: Access memory predictably](10_Per_Performance.md#Rper-access)
* [Per.30: Avoid context switches on the critical path](10_Per_Performance.md#Rper-context)

# <a name="S-concurrency"></a>CP: Concurrency and parallelism

We often want our computers to do many tasks at the same time (or at least make them appear to do them at the same time).
The reasons for doing so varies (e.g., wanting to wait for many events using only a single processor, processing many data streams simultaneously, or utilizing many hardware facilities)
and so does the basic facilities for expressing concurrency and parallelism.
Here, we articulate a few general principles and rules for using the ISO standard C++ facilities for expressing basic concurrency and parallelism.

The core machine support for concurrent and parallel programming is the thread.
Threads allow you to run multiple instances of your program independently, while sharing
the same memory. Concurrent programming is tricky for many reasons, most
importantly that it is undefined behavior to read data in one thread after it
was written by another thread, if there is no proper synchronization between
those threads. Making existing single-threaded code execute concurrently can be
as trivial as adding `std::async` or `std::thread` strategically, or it can
necessitate a full rewrite, depending on whether the original code was written
in a thread-friendly way.

The concurrency/parallelism rules in this document are designed with three goals
in mind:

* To help you write code that is amenable to being used in a threaded
  environment
* To show clean, safe ways to use the threading primitives offered by the
  standard library
* To offer guidance on what to do when concurrency and parallelism aren't giving
  you the performance gains you need

It is also important to note that concurrency in C++ is an unfinished
story. C++11 introduced many core concurrency primitives, C++14 improved on
them, and it seems that there is much interest in making the writing of
concurrent programs in C++ even easier. We expect some of the library-related
guidance here to change significantly over time.

This section needs a lot of work (obviously).
Please note that we start with rules for relative non-experts.
Real experts must wait a bit;
contributions are welcome,
but please think about the majority of programmers who are struggling to get their concurrent programs correct and performant.

Concurrency and parallelism rule summary:

* [CP.1: Assume that your code will run as part of a multi-threaded program](11_CP_Concurrency_and_parallelism.md#Rconc-multi)
* [CP.2: Avoid data races](11_CP_Concurrency_and_parallelism.md#Rconc-races)
* [CP.3: Minimize explicit sharing of writable data](11_CP_Concurrency_and_parallelism.md#Rconc-data)
* [CP.4: Think in terms of tasks, rather than threads](11_CP_Concurrency_and_parallelism.md#Rconc-task)
* [CP.8: Don't try to use `volatile` for synchronization](11_CP_Concurrency_and_parallelism.md#Rconc-volatile)
* [CP.9: Whenever feasible use tools to validate your concurrent code](11_CP_Concurrency_and_parallelism.md#Rconc-tools)

**See also**:

* [CP.con: Concurrency](11_CP_Concurrency_and_parallelism.md#SScp-con)
* [CP.par: Parallelism](11_CP_Concurrency_and_parallelism.md#SScp-par)
* [CP.mess: Message passing](11_CP_Concurrency_and_parallelism.md#SScp-mess)
* [CP.vec: Vectorization](11_CP_Concurrency_and_parallelism.md#SScp-vec)
* [CP.free: Lock-free programming](11_CP_Concurrency_and_parallelism.md#SScp-free)
* [CP.etc: Etc. concurrency rules](11_CP_Concurrency_and_parallelism.md#SScp-etc)

# <a name="S-errors"></a>E: Error handling

Error handling involves:

* Detecting an error
* Transmitting information about an error to some handler code
* Preserve the state of a program in a valid state
* Avoid resource leaks

It is not possible to recover from all errors. If recovery from an error is not possible, it is important to quickly "get out" in a well-defined way. A strategy for error handling must be simple, or it becomes a source of even worse errors.  Untested and rarely executed error-handling code is itself the source of many bugs.

The rules are designed to help avoid several kinds of errors:

* Type violations (e.g., misuse of `union`s and casts)
* Resource leaks (including memory leaks)
* Bounds errors
* Lifetime errors (e.g., accessing an object after is has been `delete`d)
* Complexity errors (logical errors made likely by overly complex expression of ideas)
* Interface errors (e.g., an unexpected value is passed through an interface)

Error-handling rule summary:

* [E.1: Develop an error-handling strategy early in a design](12_E_Error_handling.md#Re-design)
* [E.2: Throw an exception to signal that a function can't perform its assigned task](12_E_Error_handling.md#Re-throw)
* [E.3: Use exceptions for error handling only](12_E_Error_handling.md#Re-errors)
* [E.4: Design your error-handling strategy around invariants](12_E_Error_handling.md#Re-design-invariants)
* [E.5: Let a constructor establish an invariant, and throw if it cannot](12_E_Error_handling.md#Re-invariant)
* [E.6: Use RAII to prevent leaks](12_E_Error_handling.md#Re-raii)
* [E.7: State your preconditions](12_E_Error_handling.md#Re-precondition)
* [E.8: State your postconditions](12_E_Error_handling.md#Re-postcondition)

* [E.12: Use `noexcept` when exiting a function because of a `throw` is impossible or unacceptable](12_E_Error_handling.md#Re-noexcept)
* [E.13: Never throw while being the direct owner of an object](12_E_Error_handling.md#Re-never-throw)
* [E.14: Use purpose-designed user-defined types as exceptions (not built-in types)](12_E_Error_handling.md#Re-exception-types)
* [E.15: Catch exceptions from a hierarchy by reference](12_E_Error_handling.md#Re-exception-ref)
* [E.16: Destructors, deallocation, and `swap` must never fail](12_E_Error_handling.md#Re-never-fail)
* [E.17: Don't try to catch every exception in every function](12_E_Error_handling.md#Re-not-always)
* [E.18: Minimize the use of explicit `try`/`catch`](12_E_Error_handling.md#Re-catch)
* [E.19: Use a `final_action` object to express cleanup if no suitable resource handle is available](12_E_Error_handling.md#Re-finally)

* [E.25: If you can't throw exceptions, simulate RAII for resource management](12_E_Error_handling.md#Re-no-throw-raii)
* [E.26: If you can't throw exceptions, consider failing fast](12_E_Error_handling.md#Re-no-throw-crash)
* [E.27: If you can't throw exceptions, use error codes systematically](12_E_Error_handling.md#Re-no-throw-codes)
* [E.28: Avoid error handling based on global state (e.g. `errno`)](12_E_Error_handling.md#Re-no-throw)

* [E.30: Don't use exception specifications](12_E_Error_handling.md#Re-specifications)
* [E.31: Properly order your `catch`-clauses](12_E_Error_handling.md#Re_catch)

# <a name="S-const"></a>Con: Constants and immutability

You can't have a race condition on a constant.
It is easier to reason about a program when many of the objects cannot change their values.
Interfaces that promises "no change" of objects passed as arguments greatly increase readability.

Constant rule summary:

* [Con.1: By default, make objects immutable](13_Con_Constants_and_immutability.md#Rconst-immutable)
* [Con.2: By default, make member functions `const`](13_Con_Constants_and_immutability.md#Rconst-fct)
* [Con.3: By default, pass pointers and references to `const`s](13_Con_Constants_and_immutability.md#Rconst-ref)
* [Con.4: Use `const` to define objects with values that do not change after construction](13_Con_Constants_and_immutability.md#Rconst-const)
* [Con.5: Use `constexpr` for values that can be computed at compile time](13_Con_Constants_and_immutability.md#Rconst-constexpr)

# <a name="S-templates"></a>T: Templates and generic programming

Generic programming is programming using types and algorithms parameterized by types, values, and algorithms.
In C++, generic programming is supported by the `template` language mechanisms.

Arguments to generic functions are characterized by sets of requirements on the argument types and values involved.
In C++, these requirements are expressed by compile-time predicates called concepts.

Templates can also be used for meta-programming; that is, programs that compose code at compile time.

A central notion in generic programming is "concepts"; that is, requirements on template arguments presented as compile-time predicates.
"Concepts" are defined in an ISO Technical specification: [concepts](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/n4553.pdf).
A draft of a set of standard-library concepts can be found in another ISO TS: [ranges](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/n4569.pdf)
Concepts are supported in GCC 6.1 and later.
Consequently, we comment out uses of concepts in examples; that is, we use them as formalized comments only.
If you use GCC 6.1 or later, you can uncomment them.

Template use rule summary:

* [T.1: Use templates to raise the level of abstraction of code](14_T_Templates_and_generic_programming.md#Rt-raise)
* [T.2: Use templates to express algorithms that apply to many argument types](14_T_Templates_and_generic_programming.md#Rt-algo)
* [T.3: Use templates to express containers and ranges](14_T_Templates_and_generic_programming.md#Rt-cont)
* [T.4: Use templates to express syntax tree manipulation](14_T_Templates_and_generic_programming.md#Rt-expr)
* [T.5: Combine generic and OO techniques to amplify their strengths, not their costs](14_T_Templates_and_generic_programming.md#Rt-generic-oo)

Concept use rule summary:

* [T.10: Specify concepts for all template arguments](14_T_Templates_and_generic_programming.md#Rt-concepts)
* [T.11: Whenever possible use standard concepts](14_T_Templates_and_generic_programming.md#Rt-std-concepts)
* [T.12: Prefer concept names over `auto` for local variables](14_T_Templates_and_generic_programming.md#Rt-auto)
* [T.13: Prefer the shorthand notation for simple, single-type argument concepts](14_T_Templates_and_generic_programming.md#Rt-shorthand)
* ???

Concept definition rule summary:

* [T.20: Avoid "concepts" without meaningful semantics](14_T_Templates_and_generic_programming.md#Rt-low)
* [T.21: Require a complete set of operations for a concept](14_T_Templates_and_generic_programming.md#Rt-complete)
* [T.22: Specify axioms for concepts](14_T_Templates_and_generic_programming.md#Rt-axiom)
* [T.23: Differentiate a refined concept from its more general case by adding new use patterns](14_T_Templates_and_generic_programming.md#Rt-refine)
* [T.24: Use tag classes or traits to differentiate concepts that differ only in semantics](14_T_Templates_and_generic_programming.md#Rt-tag)
* [T.25: Avoid complementary constraints](14_T_Templates_and_generic_programming.md#Rt-not)
* [T.26: Prefer to define concepts in terms of use-patterns rather than simple syntax](14_T_Templates_and_generic_programming.md#Rt-use)
* [T.30: Use concept negation (`!C<T>`) sparingly to express a minor difference](14_T_Templates_and_generic_programming.md#Rt-not)
* [T.31: Use concept disjunction (`C1<T> || C2<T>`) sparingly to express alternatives](#Rt-or)
* ???

Template interface rule summary:

* [T.40: Use function objects to pass operations to algorithms](14_T_Templates_and_generic_programming.md#Rt-fo)
* [T.41: Require only essential properties in a template's concepts](14_T_Templates_and_generic_programming.md#Rt-essential)
* [T.42: Use template aliases to simplify notation and hide implementation details](14_T_Templates_and_generic_programming.md#Rt-alias)
* [T.43: Prefer `using` over `typedef` for defining aliases](14_T_Templates_and_generic_programming.md#Rt-using)
* [T.44: Use function templates to deduce class template argument types (where feasible)](14_T_Templates_and_generic_programming.md#Rt-deduce)
* [T.46: Require template arguments to be at least `Regular` or `SemiRegular`](14_T_Templates_and_generic_programming.md#Rt-regular)
* [T.47: Avoid highly visible unconstrained templates with common names](14_T_Templates_and_generic_programming.md#Rt-visible)
* [T.48: If your compiler does not support concepts, fake them with `enable_if`](14_T_Templates_and_generic_programming.md#Rt-concept-def)
* [T.49: Where possible, avoid type-erasure](14_T_Templates_and_generic_programming.md#Rt-erasure)

Template definition rule summary:

* [T.60: Minimize a template's context dependencies](14_T_Templates_and_generic_programming.md#Rt-depend)
* [T.61: Do not over-parameterize members (SCARY)](14_T_Templates_and_generic_programming.md#Rt-scary)
* [T.62: Place non-dependent class template members in a non-templated base class](14_T_Templates_and_generic_programming.md#Rt-nondependent)
* [T.64: Use specialization to provide alternative implementations of class templates](14_T_Templates_and_generic_programming.md#Rt-specialization)
* [T.65: Use tag dispatch to provide alternative implementations of functions](14_T_Templates_and_generic_programming.md#Rt-tag-dispatch)
* [T.67: Use specialization to provide alternative implementations for irregular types](14_T_Templates_and_generic_programming.md#Rt-specialization2)
* [T.68: Use `{}` rather than `()` within templates to avoid ambiguities](14_T_Templates_and_generic_programming.md#Rt-cast)
* [T.69: Inside a template, don't make an unqualified nonmember function call unless you intend it to be a customization point](14_T_Templates_and_generic_programming.md#Rt-customization)

Template and hierarchy rule summary:

* [T.80: Do not naively templatize a class hierarchy](14_T_Templates_and_generic_programming.md#Rt-hier)
* [T.81: Do not mix hierarchies and arrays](14_T_Templates_and_generic_programming.md#Rt-array) // ??? somewhere in "hierarchies"
* [T.82: Linearize a hierarchy when virtual functions are undesirable](14_T_Templates_and_generic_programming.md#Rt-linear)
* [T.83: Do not declare a member function template virtual](14_T_Templates_and_generic_programming.md#Rt-virtual)
* [T.84: Use a non-template core implementation to provide an ABI-stable interface](14_T_Templates_and_generic_programming.md#Rt-abi)
* [T.??: ????](#Rt-???)

Variadic template rule summary:

* [T.100: Use variadic templates when you need a function that takes a variable number of arguments of a variety of types](14_T_Templates_and_generic_programming.md#Rt-variadic)
* [T.101: ??? How to pass arguments to a variadic template ???](14_T_Templates_and_generic_programming.md#Rt-variadic-pass)
* [T.102: ??? How to process arguments to a variadic template ???](14_T_Templates_and_generic_programming.md#Rt-variadic-process)
* [T.103: Don't use variadic templates for homogeneous argument lists](14_T_Templates_and_generic_programming.md#Rt-variadic-not)
* [T.??: ????](#Rt-???)

Metaprogramming rule summary:

* [T.120: Use template metaprogramming only when you really need to](14_T_Templates_and_generic_programming.md#Rt-metameta)
* [T.121: Use template metaprogramming primarily to emulate concepts](14_T_Templates_and_generic_programming.md#Rt-emulate)
* [T.122: Use templates (usually template aliases) to compute types at compile time](14_T_Templates_and_generic_programming.md#Rt-tmp)
* [T.123: Use `constexpr` functions to compute values at compile time](14_T_Templates_and_generic_programming.md#Rt-fct)
* [T.124: Prefer to use standard-library TMP facilities](14_T_Templates_and_generic_programming.md#Rt-std-tmp)
* [T.125: If you need to go beyond the standard-library TMP facilities, use an existing library](14_T_Templates_and_generic_programming.md#Rt-lib)
* [T.??: ????](#Rt-???)

Other template rules summary:

* [T.140: Name all operations with potential for reuse](14_T_Templates_and_generic_programming.md#Rt-name)
* [T.141: Use an unnamed lambda if you need a simple function object in one place only](14_T_Templates_and_generic_programming.md#Rt-lambda)
* [T.142: Use template variables to simplify notation](14_T_Templates_and_generic_programming.md#Rt-var)
* [T.143: Don't write unintentionally nongeneric code](14_T_Templates_and_generic_programming.md#Rt-nongeneric)
* [T.144: Don't specialize function templates](14_T_Templates_and_generic_programming.md#Rt-specialize-function)
* [T.150: Check that a class matches a concept using `static_assert`](14_T_Templates_and_generic_programming.md#Rt-check-class)
* [T.??: ????](#Rt-???)

# <a name="S-cpl"></a>CPL: C-style programming

C and C++ are closely related languages.
They both originate in "Classic C" from 1978 and have evolved in ISO committees since then.
Many attempts have been made to keep them compatible, but neither is a subset of the other.

C rule summary:

* [CPL.1: Prefer C++ to C](15_CPL_C-style_programming.md#Rcpl-C)
* [CPL.2: If you must use C, use the common subset of C and C++, and compile the C code as C++](15_CPL_C-style_programming.md#Rcpl-subset)
* [CPL.3: If you must use C for interfaces, use C++ in the calling code using such interfaces](15_CPL_C-style_programming.md#Rcpl-interface)

# <a name="S-source"></a>SF: Source files

Distinguish between declarations (used as interfaces) and definitions (used as implementations).
Use header files to represent interfaces and to emphasize logical structure.

Source file rule summary:

* [SF.1: Use a `.cpp` suffix for code files and `.h` for interface files if your project doesn't already follow another convention](16_SF_Source_files.md#Rs-file-suffix)
* [SF.2: A `.h` file may not contain object definitions or non-inline function definitions](16_SF_Source_files.md#Rs-inline)
* [SF.3: Use `.h` files for all declarations used in multiple source files](16_SF_Source_files.md#Rs-declaration-header)
* [SF.4: Include `.h` files before other declarations in a file](16_SF_Source_files.md#Rs-include-order)
* [SF.5: A `.cpp` file must include the `.h` file(s) that defines its interface](16_SF_Source_files.md#Rs-consistency)
* [SF.6: Use `using namespace` directives for transition, for foundation libraries (such as `std`), or within a local scope (only)](16_SF_Source_files.md#Rs-using)
* [SF.7: Don't write `using namespace` at global scope in a header file](16_SF_Source_files.md#Rs-using-directive)
* [SF.8: Use `#include` guards for all `.h` files](16_SF_Source_files.md#Rs-guards)
* [SF.9: Avoid cyclic dependencies among source files](16_SF_Source_files.md#Rs-cycles)
* [SF.10: Avoid dependencies on implicitly `#include`d names](16_SF_Source_files.md#Rs-implicit)
* [SF.11: Header files should be self-contained](16_SF_Source_files.md#Rs-contained)

* [SF.20: Use `namespace`s to express logical structure](16_SF_Source_files.md#Rs-namespace)
* [SF.21: Don't use an unnamed (anonymous) namespace in a header](16_SF_Source_files.md#Rs-unnamed)
* [SF.22: Use an unnamed (anonymous) namespace for all internal/nonexported entities](16_SF_Source_files.md#Rs-unnamed2)

# <a name="S-stdlib"></a>SL: The Standard Library

Using only the bare language, every task is tedious (in any language).
Using a suitable library any task can be reasonably simple.

The standard library has steadily grown over the years.
Its description in the standard is now larger than that of the language features.
So, it is likely that this library section of the guidelines will eventually grow in size to equal or exceed all the rest.

<< ??? We need another level of rule numbering ??? >>

C++ Standard Library component summary:

* [SL.con: Containers](17_SL_The_Standard_Library.md#SS-con)
* [SL.str: String](17_SL_The_Standard_Library.md#SS-string)
* [SL.io: Iostream](17_SL_The_Standard_Library.md#SS-io)
* [SL.regex: Regex](17_SL_The_Standard_Library.md#SS-regex)
* [SL.chrono: Time](17_SL_The_Standard_Library.md#SS-chrono)
* [SL.C: The C Standard Library](17_SL_The_Standard_Library.md#SS-clib)

Standard-library rule summary:

* [SL.1: Use libraries wherever possible](17_SL_The_Standard_Library.md#Rsl-lib)
* [SL.2: Prefer the standard library to other libraries](17_SL_The_Standard_Library.md#Rsl-sl)
* [SL.3: Do not add non-standard entities to namespace `std`](17_SL_The_Standard_Library.md#sl-std)
* [SL.4: Use the standard library in a type-safe manner](17_SL_The_Standard_Library.md#sl-safe)
* ???

# <a name="S-A"></a>A: Architectural ideas

This section contains ideas about higher-level architectural ideas and libraries.

Architectural rule summary:

* [A.1: Separate stable from less stable part of code](18_A_Architectural_ideas.md#Ra-stable)
* [A.2: Express potentially reusable parts as a library](18_A_Architectural_ideas.md#Ra-lib)
* [A.4: There should be no cycles among libraries](18_A_Architectural_ideas.md#Ra-dag)
* [???](#???)
* [???](#???)
* [???](#???)
* [???](#???)
* [???](#???)
* [???](#???)

# <a name="S-not"></a>NR: Non-Rules and myths

This section contains rules and guidelines that are popular somewhere, but that we deliberately don't recommend.
We know full well that there have been times and places where these rules made sense, and we have used them ourselves at times.
However, in the context of the styles of programming we recommend and support with the guidelines, these "non-rules" would do harm.

Even today, there can be contexts where the rules make sense.
For example, lack of suitable tool support can make exceptions unsuitable in hard-real-time systems,
but please don't blindly trust "common wisdom" (e.g., unsupported statements about "efficiency");
such "wisdom" may be based on decades-old information or experienced from languages with very different properties than C++
(e.g., C or Java).

The positive arguments for alternatives to these non-rules are listed in the rules offered as "Alternatives".

Non-rule summary:

* [NR.1: Don't: All declarations should be at the top of a function](19_NR_Non-Rules_and_myths.md#Rnr-top)
* [NR.2: Don't: Have only a single `return`-statement in a function](19_NR_Non-Rules_and_myths.md#Rnr-single-return)
* [NR.3: Don't: Don't use exceptions](19_NR_Non-Rules_and_myths.md#Rnr-no-exceptions)
* [NR.4: Don't: Place each class declaration in its own source file](19_NR_Non-Rules_and_myths.md#Rnr-lots-of-files)
* [NR.5: Don't: Don't do substantive work in a constructor; instead use two-phase initialization](19_NR_Non-Rules_and_myths.md#Rnr-two-phase-init)
* [NR.6: Don't: Place all cleanup actions at the end of a function and `goto exit`](19_NR_Non-Rules_and_myths.md#Rnr-goto-exit)
* [NR.7: Don't: Make all data members `protected`](19_NR_Non-Rules_and_myths.md#Rnr-protected-data)
* ???

# <a name="S-references"></a>RF: References

Many coding standards, rules, and guidelines have been written for C++, and especially for specialized uses of C++.
Many

* focus on lower-level issues, such as the spelling of identifiers
* are written by C++ novices
* see "stopping programmers from doing unusual things" as their primary aim
* aim at portability across many compilers (some 10 years old)
* are written to preserve decades old code bases
* aim at a single application domain
* are downright counterproductive
* are ignored (must be ignored by programmers to get their work done well)

A bad coding standard is worse than no coding standard.
However an appropriate set of guidelines are much better than no standards: "Form is liberating."

Why can't we just have a language that allows all we want and disallows all we don't want ("a perfect language")?
Fundamentally, because affordable languages (and their tool chains) also serve people with needs that differ from yours and serve more needs than you have today.
Also, your needs change over time and a general-purpose language is needed to allow you to adapt.
A language that is ideal for today would be overly restrictive tomorrow.

Coding guidelines adapt the use of a language to specific needs.
Thus, there cannot be a single coding style for everybody.
We expect different organizations to provide additions, typically with more restrictions and firmer style rules.

Reference sections:

* [RF.rules: Coding rules](20_RF_References.md#SS-rules)
* [RF.books: Books with coding guidelines](20_RF_References.md#SS-books)
* [RF.C++: C++ Programming (C++11/C++14)](20_RF_References.md#SS-Cplusplus)
* [RF.web: Websites](20_RF_References.md#SS-web)
* [RS.video: Videos about "modern C++"](20_RF_References.md#SS-vid)
* [RF.man: Manuals](20_RF_References.md#SS-man)
* [RF.core: Core Guidelines materials](20_RF_References.md#SS-core)

# <a name="S-profile"></a>Pro: Profiles

Ideally, we would follow all of the guidelines.
That would give the cleanest, most regular, least error-prone, and often the fastest code.
Unfortunately, that is usually impossible because we have to fit our code into large code bases and use existing libraries.
Often, such code has been written over decades and does not follow these guidelines.
We must aim for [gradual adoption](01_main.md#S-modernizing).

Whatever strategy for gradual adoption we adopt, we need to be able to apply sets of related guidelines to address some set
of problems first and leave the rest until later.
A similar idea of "related guidelines" becomes important when some, but not all, guidelines are considered relevant to a code base
or if a set of specialized guidelines is to be applied for a specialized application area.
We call such a set of related guidelines a "profile".
We aim for such a set of guidelines to be coherent so that they together help us reach a specific goal, such as "absence of range errors"
or "static type safety."
Each profile is designed to eliminate a class of errors.
Enforcement of "random" rules in isolation is more likely to be disruptive to a code base than delivering a definite improvement.

A "profile" is a set of deterministic and portably enforceable subset rules (i.e., restrictions) that are designed to achieve a specific guarantee.
"Deterministic" means they require only local analysis and could be implemented in a compiler (though they don't need to be).
"Portably enforceable" means they are like language rules, so programmers can count on different enforcement tools giving the same answer for the same code.

Code written to be warning-free using such a language profile is considered to conform to the profile.
Conforming code is considered to be safe by construction with regard to the safety properties targeted by that profile.
Conforming code will not be the root cause of errors for that property,
although such errors may be introduced into a program by other code, libraries or the external environment.
A profile may also introduce additional library types to ease conformance and encourage correct code.

Profiles summary:

* [Pro.type: Type safety](21_Pro_Profiles.md#SS-type)
* [Pro.bounds: Bounds safety](21_Pro_Profiles.md#SS-bounds)
* [Pro.lifetime: Lifetime safety](21_Pro_Profiles.md#SS-lifetime)

In the future, we expect to define many more profiles and add more checks to existing profiles.
Candidates include:

* narrowing arithmetic promotions/conversions (likely part of a separate safe-arithmetic profile)
* arithmetic cast from negative floating point to unsigned integral type (ditto)
* selected undefined behavior: Start with Gabriel Dos Reis's UB list developed for the WG21 study group
* selected unspecified behavior: Addressing portability concerns.
* `const` violations: Mostly done by compilers already, but we can catch inappropriate casting and underuse of `const`.

Enabling a profile is implementation defined; typically, it is set in the analysis tool used.

To suppress enforcement of a profile check, place a `suppress` annotation on a language contract. For example:

    [[suppress(bounds)]] char* raw_find(char* p, int n, char x)    // find x in p[0]..p[n - 1]
    {
        // ...
    }

Now `raw_find()` can scramble memory to its heart's content.
Obviously, suppression should be very rare.

# <a name="S-gsl"></a>GSL: Guidelines support library

The GSL is a small library of facilities designed to support this set of guidelines.
Without these facilities, the guidelines would have to be far more restrictive on language details.

The Core Guidelines support library is defined in namespace `gsl` and the names may be aliases for standard library or other well-known library names. Using the (compile-time) indirection through the `gsl` namespace allows for experimentation and for local variants of the support facilities.

The GSL is header only, and can be found at [GSL: Guidelines support library](https://github.com/Microsoft/GSL).
The support library facilities are designed to be extremely lightweight (zero-overhead) so that they impose no overhead compared to using conventional alternatives.
Where desirable, they can be "instrumented" with additional functionality (e.g., checks) for tasks such as debugging.

These Guidelines assume a `variant` type, but this is not currently in GSL.
Eventually, use [the one voted into C++17](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0088r3.html).

Summary of GSL components:

* [GSL.view: Views](22_GSL_Guidelines_support_library.md#SS-views)
* [GSL.owner](22_GSL_Guidelines_support_library.md#SS-ownership)
* [GSL.assert: Assertions](22_GSL_Guidelines_support_library.md#SS-assertions)
* [GSL.util: Utilities](22_GSL_Guidelines_support_library.md#SS-utilities)
* [GSL.concept: Concepts](22_GSL_Guidelines_support_library.md#SS-gsl-concepts)

We plan for a "ISO C++ standard style" semi-formal specification of the GSL.

We rely on the ISO C++ Standard Library and hope for parts of the GSL to be absorbed into the standard library.

# <a name="S-naming"></a>NL: Naming and layout rules

Consistent naming and layout are helpful.
If for no other reason because it minimizes "my style is better than your style" arguments.
However, there are many, many, different styles around and people are passionate about them (pro and con).
Also, most real-world projects includes code from many sources, so standardizing on a single style for all code is often impossible.
We present a set of rules that you might use if you have no better ideas, but the real aim is consistency, rather than any particular rule set.
IDEs and tools can help (as well as hinder).

Naming and layout rules:

* [NL.1: Don't say in comments what can be clearly stated in code](23_NL_Naming_and_layout_rules.md#Rl-comments)
* [NL.2: State intent in comments](23_NL_Naming_and_layout_rules.md#Rl-comments-intent)
* [NL.3: Keep comments crisp](23_NL_Naming_and_layout_rules.md#Rl-comments-crisp)
* [NL.4: Maintain a consistent indentation style](23_NL_Naming_and_layout_rules.md#Rl-indent)
* [NL.5: Avoid encoding type information in names](23_NL_Naming_and_layout_rules.md#Rl-name-type)
* [NL.7: Make the length of a name roughly proportional to the length of its scope](23_NL_Naming_and_layout_rules.md#Rl-name-length)
* [NL.8: Use a consistent naming style](23_NL_Naming_and_layout_rules.md#Rl-name)
* [NL.9: Use `ALL_CAPS` for macro names only](23_NL_Naming_and_layout_rules.md#Rl-all-caps)
* [NL.10: Prefer `underscore_style` names](23_NL_Naming_and_layout_rules.md#Rl-camel)
* [NL.11: Make literals readable](23_NL_Naming_and_layout_rules.md#Rl-literals)
* [NL.15: Use spaces sparingly](23_NL_Naming_and_layout_rules.md#Rl-space)
* [NL.16: Use a conventional class member declaration order](23_NL_Naming_and_layout_rules.md#Rl-order)
* [NL.17: Use K&R-derived layout](23_NL_Naming_and_layout_rules.md#Rl-knr)
* [NL.18: Use C++-style declarator layout](23_NL_Naming_and_layout_rules.md#Rl-ptr)
* [NL.19: Avoid names that are easily misread](23_NL_Naming_and_layout_rules.md#Rl-misread)
* [NL.20: Don't place two statements on the same line](23_NL_Naming_and_layout_rules.md#Rl-stmt)
* [NL.21: Declare one name (only) per declaration](23_NL_Naming_and_layout_rules.md#Rl-dcl)
* [NL.25: Don't use `void` as an argument type](23_NL_Naming_and_layout_rules.md#Rl-void)
* [NL.26: Use conventional `const` notation](23_NL_Naming_and_layout_rules.md#Rl-const)

Most of these rules are aesthetic and programmers hold strong opinions.
IDEs also tend to have defaults and a range of alternatives.
These rules are suggested defaults to follow unless you have reasons not to.

We have had comments to the effect that naming and layout are so personal and/or arbitrary that we should not try to "legislate" them.
We are not "legislating" (see the previous paragraph).
However, we have had many requests for a set of naming and layout conventions to use when there are no external constraints.

More specific and detailed rules are easier to enforce.

These rules bear a strong resemblance to the recommendations in the [PPP Style Guide](http://www.stroustrup.com/Programming/PPP-style.pdf)
written in support of Stroustrup's [Programming: Principles and Practice using C++](http://www.stroustrup.com/programming.html).

# <a name="S-faq"></a>FAQ: Answers to frequently asked questions

This section covers answers to frequently asked questions about these guidelines.

# <a name="S-libraries"></a>Appendix A: Libraries

This section lists recommended libraries, and explicitly recommends a few.

??? Suitable for the general guide? I think not ???

# <a name="S-modernizing"></a>Appendix B: Modernizing code

Ideally, we follow all rules in all code.
Realistically, we have to deal with a lot of old code:

* application code written before the guidelines were formulated or known
* libraries written to older/different standards
* code written under "unusual" constraints
* code that we just haven't gotten around to modernizing

If we have a million lines of new code, the idea of "just changing it all at once" is typically unrealistic.
Thus, we need a way of gradually modernizing a code base.

Upgrading older code to modern style can be a daunting task.
Often, the old code is both a mess (hard to understand) and working correctly (for the current range of uses).
Typically, the original programmer is not around and the test cases incomplete.
The fact that the code is a mess dramatically increases the effort needed to make any change and the risk of introducing errors.
Often, messy old code runs unnecessarily slowly because it requires outdated compilers and cannot take advantage of modern hardware.
In many cases, automated "modernizer"-style tool support would be required for major upgrade efforts.

The purpose of modernizing code is to simplify adding new functionality, to ease maintenance, and to increase performance (throughput or latency), and to better utilize modern hardware.
Making code "look pretty" or "follow modern style" are not by themselves reasons for change.
There are risks implied by every change and costs (including the cost of lost opportunities) implied by having an outdated code base.
The cost reductions must outweigh the risks.

But how?

There is no one approach to modernizing code.
How best to do it depends on the code, the pressure for updates, the backgrounds of the developers, and the available tool.
Here are some (very general) ideas:

* The ideal is "just upgrade everything." That gives the most benefits for the shortest total time.
  In most circumstances, it is also impossible.
* We could convert a code base module for module, but any rules that affects interfaces (especially ABIs), such as [use `span`](22_GSL_Guidelines_support_library.md#SS-views), cannot be done on a per-module basis.
* We could convert code "bottom up" starting with the rules we estimate will give the greatest benefits and/or the least trouble in a given code base.
* We could start by focusing on the interfaces, e.g., make sure that no resources are lost and no pointer is misused.
  This would be a set of changes across the whole code base, but would most likely have huge benefits.
  Afterwards, code hidden behind those interfaces can be gradually modernized without affecting other code.

Whichever way you choose, please note that the most advantages come with the highest conformance to the guidelines.
The guidelines are not a random set of unrelated rules where you can randomly pick and choose with an expectation of success.

We would dearly love to hear about experience and about tools used.
Modernization can be much faster, simpler, and safer when supported with analysis tools and even code transformation tools.

# <a name="S-discussion"></a>Appendix C: Discussion

This section contains follow-up material on rules and sets of rules.
In particular, here we present further rationale, longer examples, and discussions of alternatives.

# <a name="S-tools"></a>Appendix D: Supporting tools

This section contains a list of tools that directly support adoption of the C++ Core Guidelines. This list is not intended to be an exhaustive list of tools
that are helpful in writing good C++ code. If a tool is designed specifically to support and links to the C++ Core Guidelines it is a candidate for inclusion.

# <a name="S-glossary"></a>Glossary

A relatively informal definition of terms used in the guidelines
(based of the glossary in [Programming: Principles and Practice using C++](http://www.stroustrup.com/programming.html))

More information on many topics about C++ can be found on the [Standard C++ Foundation](https://isocpp.org)'s site.

* *ABI*: Application Binary Interface, a specification for a specific hardware platform combined with the operating system. Contrast with API.
* *abstract class*: a class that cannot be directly used to create objects; often used to define an interface to derived classes.
  A class is made abstract by having a pure virtual function or only protected constructors.
* *abstraction*: a description of something that selectively and deliberately ignores (hides) details (e.g., implementation details); selective ignorance.
* *address*: a value that allows us to find an object in a computer's memory.
* *algorithm*: a procedure or formula for solving a problem; a finite series of computational steps to produce a result.
* *alias*: an alternative way of referring to an object; often a name, pointer, or reference.
* *API*: Application Programming Interface, a set of functions that form the communication between various software components. Contrast with ABI.
* *application*: a program or a collection of programs that is considered an entity by its users.
* *approximation*: something (e.g., a value or a design) that is close to the perfect or ideal (value or design).
  Often an approximation is a result of trade-offs among ideals.
* *argument*: a value passed to a function or a template, in which it is accessed through a parameter.
* *array*: a homogeneous sequence of elements, usually numbered, e.g., `[0:max)`.
* *assertion*: a statement inserted into a program to state (assert) that something must always be true at this point in the program.
* *base class*: a class used as the base of a class hierarchy. Typically a base class has one or more virtual functions.
* *bit*: the basic unit of information in a computer. A bit can have the value 0 or the value 1.
* *bug*: an error in a program.
* *byte*: the basic unit of addressing in most computers. Typically, a byte holds 8 bits.
* *class*: a user-defined type that may contain data members, function members, and member types.
* *code*: a program or a part of a program; ambiguously used for both source code and object code.
* *compiler*: a program that turns source code into object code.
* *complexity*: a hard-to-precisely-define notion or measure of the difficulty of constructing a solution to a problem or of the solution itself.
  Sometimes complexity is used to (simply) mean an estimate of the number of operations needed to execute an algorithm.
* *computation*: the execution of some code, usually taking some input and producing some output.
* *concept*: (1) a notion, and idea; (2) a set of requirements, usually for a template argument.
* *concrete class*: class for which objects can be created.
* *constant*: a value that cannot be changed (in a given scope); not mutable.
* *constructor*: an operation that initializes ("constructs") an object.
  Typically a constructor establishes an invariant and often acquires resources needed for an object to be used (which are then typically released by a destructor).
* *container*: an object that holds elements (other objects).
* *copy*: an operation that makes two object have values that compare equal. See also move.
* *correctness*: a program or a piece of a program is correct if it meets its specification.
  Unfortunately, a specification can be incomplete or inconsistent, or can fail to meet users' reasonable expectations.
  Thus, to produce acceptable code, we sometimes have to do more than just follow the formal specification.
* *cost*: the expense (e.g., in programmer time, run time, or space) of producing a program or of executing it.
  Ideally, cost should be a function of complexity.
* *customization point*: ???
* *data*: values used in a computation.
* *debugging*: the act of searching for and removing errors from a program; usually far less systematic than testing.
* *declaration*: the specification of a name with its type in a program.
* *definition*: a declaration of an entity that supplies all information necessary to complete a program using the entity.
  Simplified definition: a declaration that allocates memory.
* *derived class*: a class derived from one or more base classes.
* *design*: an overall description of how a piece of software should operate to meet its specification.
* *destructor*: an operation that is implicitly invoked (called) when an object is destroyed (e.g., at the end of a scope). Often, it releases resources.
* *encapsulation*: protecting something meant to be private (e.g., implementation details) from unauthorized access.
* *error*: a mismatch between reasonable expectations of program behavior (often expressed as a requirement or a users' guide) and what a program actually does.
* *executable*: a program ready to be run (executed) on a computer.
* *feature creep*: a tendency to add excess functionality to a program "just in case."
* *file*: a container of permanent information in a computer.
* *floating-point number*: a computer's approximation of a real number, such as 7.93 and 10.78e-3.
* *function*: a named unit of code that can be invoked (called) from different parts of a program; a logical unit of computation.
* *generic programming*: a style of programming focused on the design and efficient implementation of algorithms.
  A generic algorithm will work for all argument types that meet its requirements. In C++, generic programming typically uses templates.
* *global variable*: technically, a named object in namespace scope.
* *handle*: a class that allows access to another through a member pointer or reference. See also resource, copy, move.
* *header*: a file containing declarations used to share interfaces between parts of a program.
* *hiding*: the act of preventing a piece of information from being directly seen or accessed.
  For example, a name from a nested (inner) scope can prevent that same name from an outer (enclosing) scope from being directly used.
* *ideal*: the perfect version of something we are striving for. Usually we have to make trade-offs and settle for an approximation.
* *implementation*: (1) the act of writing and testing code; (2) the code that implements a program.
* *infinite loop*: a loop where the termination condition never becomes true. See iteration.
* *infinite recursion*: a recursion that doesn't end until the machine runs out of memory to hold the calls.
  In reality, such recursion is never infinite but is terminated by some hardware error.
* *information hiding*: the act of separating interface and implementation, thus hiding implementation details not meant for the user's attention and providing an abstraction.
* *initialize*: giving an object its first (initial) value.
* *input*: values used by a computation (e.g., function arguments and characters typed on a keyboard).
* *integer*: a whole number, such as 42 and -99.
* *interface*: a declaration or a set of declarations specifying how a piece of code (such as a function or a class) can be called.
* *invariant*: something that must be always true at a given point (or points) of a program; typically used to describe the state (set of values) of an object or the state of a loop before entry into the repeated statement.
* *iteration*: the act of repeatedly executing a piece of code; see recursion.
* *iterator*: an object that identifies an element of a sequence.
* *ISO*: International Organization for Standardization. The C++ language is an ISO standard, ISO/IEC 14882. More information at [iso.org](http://iso.org).
* *library*: a collection of types, functions, classes, etc. implementing a set of facilities (abstractions) meant to be potentially used as part of more that one program.
* *lifetime*: the time from the initialization of an object until it becomes unusable (goes out of scope, is deleted, or the program terminates).
* *linker*: a program that combines object code files and libraries into an executable program.
* *literal*: a notation that directly specifies a value, such as 12 specifying the integer value "twelve."
* *loop*: a piece of code executed repeatedly; in C++, typically a for-statement or a `while`-statement.
* *move*: an operation that transfers a value from one object to another leaving behind a value representing "empty." See also copy.
* *mutable*: changeable; the opposite of immutable, constant, and invariable.
* *object*: (1) an initialized region of memory of a known type which holds a value of that type; (2) a region of memory.
* *object code*: output from a compiler intended as input for a linker (for the linker to produce executable code).
* *object file*: a file containing object code.
* *object-oriented programming*: (OOP) a style of programming focused on the design and use of classes and class hierarchies.
* *operation*: something that can perform some action, such as a function and an operator.
* *output*: values produced by a computation (e.g., a function result or lines of characters written on a screen).
* *overflow*: producing a value that cannot be stored in its intended target.
* *overload*: defining two functions or operators with the same name but different argument (operand) types.
* *override*: defining a function in a derived class with the same name and argument types as a virtual function in the base class, thus making the function callable through the interface defined by the base class.
* *owner*: an object responsible for releasing a resource.
* *paradigm*: a somewhat pretentious term for design or programming style; often used with the (erroneous) implication that there exists a paradigm that is superior to all others.
* *parameter*: a declaration of an explicit input to a function or a template. When called, a function can access the arguments passed through the names of its parameters.
* *pointer*: (1) a value used to identify a typed object in memory; (2) a variable holding such a value.
* *post-condition*: a condition that must hold upon exit from a piece of code, such as a function or a loop.
* *pre-condition*: a condition that must hold upon entry into a piece of code, such as a function or a loop.
* *program*: code (possibly with associated data) that is sufficiently complete to be executed by a computer.
* *programming*: the art of expressing solutions to problems as code.
* *programming language*: a language for expressing programs.
* *pseudo code*: a description of a computation written in an informal notation rather than a programming language.
* *pure virtual function*: a virtual function that must be overridden in a derived class.
* *RAII*: ("Resource Acquisition Is Initialization") a basic technique for resource management based on scopes.
* *range*: a sequence of values that can be described by a start point and an end point. For example, `[0:5)` means the values 0, 1, 2, 3, and 4.
* *recursion*: the act of a function calling itself; see also iteration.
* *reference*: (1) a value describing the location of a typed value in memory; (2) a variable holding such a value.
* *regular expression*: a notation for patterns in character strings.
* *regular*: a type that behaves similarly to built-in types like `int` and can be compared with `==`.
In particular, an object of a regular type can be copied and the result of a copy is a separate object that compares equal to the original. See also *semiregular type*.
* *requirement*: (1) a description of the desired behavior of a program or part of a program; (2) a description of the assumptions a function or template makes of its arguments.
* *resource*: something that is acquired and must later be released, such as a file handle, a lock, or memory. See also handle, owner.
* *rounding*: conversion of a value to the mathematically nearest value of a less precise type.
* *RTTI*: Run-Time Type Information. ???
* *scope*: the region of program text (source code) in which a name can be referred to.
* *semiregular*: a type that behaves roughly like an built-in type like `int`, but possibly without a `==` operator. See also *regular type*.
* *sequence*: elements that can be visited in a linear order.
* *software*: a collection of pieces of code and associated data; often used interchangeably with program.
* *source code*: code as produced by a programmer and (in principle) readable by other programmers.
* *source file*: a file containing source code.
* *specification*: a description of what a piece of code should do.
* *standard*: an officially agreed upon definition of something, such as a programming language.
* *state*: a set of values.
* *STL*: the containers, iterators, and algorithms part of the standard library.
* *string*: a sequence of characters.
* *style*: a set of techniques for programming leading to a consistent use of language features; sometimes used in a very restricted sense to refer just to low-level rules for naming and appearance of code.
* *subtype*: derived type; a type that has all the properties of a type and possibly more.
* *supertype*: base type; a type that has a subset of the properties of a type.
* *system*: (1) a program or a set of programs for performing a task on a computer; (2) a shorthand for "operating system", that is, the fundamental execution environment and tools for a computer.
* *TS*: [Technical Specification](https://www.iso.org/deliverables-all.html?type=ts), A Technical Specification addresses work still under technical development, or where it is believed that there will be a future, but not immediate, possibility of agreement on an International Standard. A Technical Specification is published for immediate use, but it also provides a means to obtain feedback. The aim is that it will eventually be transformed and republished as an International Standard.
* *template*: a class or a function parameterized by one or more types or (compile-time) values; the basic C++ language construct supporting generic programming.
* *testing*: a systematic search for errors in a program.
* *trade-off*: the result of balancing several design and implementation criteria.
* *truncation*: loss of information in a conversion from a type into another that cannot exactly represent the value to be converted.
* *type*: something that defines a set of possible values and a set of operations for an object.
* *uninitialized*: the (undefined) state of an object before it is initialized.
* *unit*: (1) a standard measure that gives meaning to a value (e.g., km for a distance); (2) a distinguished (e.g., named) part of a larger whole.
* *use case*: a specific (typically simple) use of a program meant to test its functionality and demonstrate its purpose.
* *value*: a set of bits in memory interpreted according to a type.
* *variable*: a named object of a given type; contains a value unless uninitialized.
* *virtual function*: a member function that can be overridden in a derived class.
* *word*: a basic unit of memory in a computer, often the unit used to hold an integer.

# <a name="S-unclassified"></a>To-do: Unclassified proto-rules

This is our to-do list.
Eventually, the entries will become rules or parts of rules.
Alternatively, we will decide that no change is needed and delete the entry.

* No long-distance friendship
* Should physical design (what's in a file) and large-scale design (libraries, groups of libraries) be addressed?
* Namespaces
* Avoid using directives in the global scope (except for std, and other "fundamental" namespaces (e.g. experimental))
* How granular should namespaces be? All classes/functions designed to work together and released together (as defined in Sutter/Alexandrescu) or something narrower or wider?
* Should there be inline namespaces (à la `std::literals::*_literals`)?
* Avoid implicit conversions
* Const member functions should be thread safe ... aka, but I don't really change the variable, just assign it a value the first time it's called ... argh
* Always initialize variables, use initialization lists for member variables.
* Anyone writing a public interface which takes or returns `void*` should have their toes set on fire. That one has been a personal favorite of mine for a number of years. :)
* Use `const`-ness wherever possible: member functions, variables and (yippee) `const_iterators`
* Use `auto`
* `(size)` vs. `{initializers}` vs. `{Extent{size}}`
* Don't overabstract
* Never pass a pointer down the call stack
* falling through a function bottom
* Should there be guidelines to choose between polymorphisms? YES. classic (virtual functions, reference semantics) vs. Sean Parent style (value semantics, type-erased, kind of like `std::function`)  vs. CRTP/static? YES Perhaps even vs. tag dispatch?
* should virtual calls be banned from ctors/dtors in your guidelines? YES. A lot of people ban them, even though I think it's a big strength of C++ that they are ??? -preserving (D disappointed me so much when it went the Java way). WHAT WOULD BE A GOOD EXAMPLE?
* Speaking of lambdas, what would weigh in on the decision between lambdas and (local?) classes in algorithm calls and other callback scenarios?
* And speaking of `std::bind`, Stephen T. Lavavej criticizes it so much I'm starting to wonder if it is indeed going to fade away in future. Should lambdas be recommended instead?
* What to do with leaks out of temporaries? : `p = (s1 + s2).c_str();`
* pointer/iterator invalidation leading to dangling pointers:

        void bad()
        {
            int* p = new int[700];
            int* q = &p[7];
            delete p;

            vector<int> v(700);
            int* q2 = &v[7];
            v.resize(900);

            // ... use q and q2 ...
        }

* LSP
* private inheritance vs/and membership
* avoid static class members variables (race conditions, almost-global variables)

* Use RAII lock guards (`lock_guard`, `unique_lock`, `shared_lock`), never call `mutex.lock` and `mutex.unlock` directly (RAII)
* Prefer non-recursive locks (often used to work around bad reasoning, overhead)
* Join your threads! (because of `std::terminate` in destructor if not joined or detached ... is there a good reason to detach threads?) -- ??? could support library provide a RAII wrapper for `std::thread`?
* If two or more mutexes must be acquired at the same time, use `std::lock` (or another deadlock avoidance algorithm?)
* When using a `condition_variable`, always protect the condition by a mutex (atomic bool whose value is set outside of the mutex is wrong!), and use the same mutex for the condition variable itself.
* Never use `atomic_compare_exchange_strong` with `std::atomic<user-defined-struct>` (differences in padding matter, while `compare_exchange_weak` in a loop converges to stable padding)
* individual `shared_future` objects are not thread-safe: two threads cannot wait on the same `shared_future` object (they can wait on copies of a `shared_future` that refer to the same shared state)
* individual `shared_ptr` objects are not thread-safe: different threads can call non-`const` member functions on *different* `shared_ptr`s that refer to the same shared object, but one thread cannot call a non-`const` member function of a `shared_ptr` object while another thread accesses that same `shared_ptr` object (if you need that, consider `atomic_shared_ptr` instead)

* rules for arithmetic

# Bibliography

* <a name="Abrahams01"></a>
  \[Abrahams01]:  D. Abrahams. [Exception-Safety in Generic Components](http://www.boost.org/community/exception_safety.html).
* <a name="Alexandrescu01"></a>
  \[Alexandrescu01]:  A. Alexandrescu. Modern C++ Design (Addison-Wesley, 2001).
* <a name="Cplusplus03"></a>
  \[C++03]:           ISO/IEC 14882:2003(E), Programming Languages — C++ (updated ISO and ANSI C++ Standard including the contents of (C++98) plus errata corrections).
* <a name="CplusplusCS"></a>
  \[C++CS]:           ???
* <a name="Cargill92"></a>
  \[Cargill92]:       T. Cargill. C++ Programming Style (Addison-Wesley, 1992).
* <a name="Cline99"></a>
  \[Cline99]:         M. Cline, G. Lomow, and M. Girou. C++ FAQs (2ndEdition) (Addison-Wesley, 1999).
* <a name="Dewhurst03"></a>
  \[Dewhurst03]:      S. Dewhurst. C++ Gotchas (Addison-Wesley, 2003).
* <a name="Henricson97"></a>
  \[Henricson97]:     M. Henricson and E. Nyquist. Industrial Strength C++ (Prentice Hall, 1997).
* <a name="Koenig97"></a>
  \[Koenig97]:        A. Koenig and B. Moo. Ruminations on C++ (Addison-Wesley, 1997).
* <a name="Lakos96"></a>
  \[Lakos96]:         J. Lakos. Large-Scale C++ Software Design (Addison-Wesley, 1996).
* <a name="Meyers96"></a>
  \[Meyers96]:        S. Meyers. More Effective C++ (Addison-Wesley, 1996).
* <a name="Meyers97"></a>
  \[Meyers97]:        S. Meyers. Effective C++ (2nd Edition) (Addison-Wesley, 1997).
* <a name="Meyers15"></a>
  \[Meyers15]:        S. Meyers. Effective Modern C++ (O'Reilly, 2015).
* <a name="Murray93"></a>
  \[Murray93]:        R. Murray. C++ Strategies and Tactics (Addison-Wesley, 1993).
* <a name="Stroustrup94"></a>
  \[Stroustrup94]:    B. Stroustrup. The Design and Evolution of C++ (Addison-Wesley, 1994).
* <a name="Stroustrup00"></a>
  \[Stroustrup00]:    B. Stroustrup. The C++ Programming Language (Special 3rdEdition) (Addison-Wesley, 2000).
* <a name="Stroustrup05"></a>
  \[Stroustrup05]:    B. Stroustrup. [A rationale for semantically enhanced library languages](http://www.stroustrup.com/SELLrationale.pdf).
* <a name="Stroustrup13"></a>
  \[Stroustrup13]:    B. Stroustrup. [The C++ Programming Language (4th Edition)](http://www.stroustrup.com/4th.html). Addison Wesley 2013.
* <a name="Stroustrup14"></a>
  \[Stroustrup14]:    B. Stroustrup. [A Tour of C++](http://www.stroustrup.com/Tour.html).
  Addison Wesley 2014.
* <a name="Stroustrup15"></a>
  \[Stroustrup15]:    B. Stroustrup, Herb Sutter, and G. Dos Reis: [A brief introduction to C++'s model for type- and resource-safety](https://github.com/isocpp/CppCoreGuidelines/blob/master/docs/Introduction%20to%20type%20and%20resource%20safety.pdf).
* <a name="SuttHysl04b"></a>
  \[SuttHysl04b]:     H. Sutter and J. Hyslop. "Collecting Shared Objects" (C/C++ Users Journal, 22(8), August 2004).
* <a name="SuttAlex05"></a>
  \[SuttAlex05]:      H. Sutter and  A. Alexandrescu. C++ Coding Standards. Addison-Wesley 2005.
* <a name="Sutter00"></a>
  \[Sutter00]:        H. Sutter. Exceptional C++ (Addison-Wesley, 2000).
* <a name="Sutter02"></a>
  \[Sutter02]:        H. Sutter. More Exceptional C++ (Addison-Wesley, 2002).
* <a name="Sutter04"></a>
  \[Sutter04]:        H. Sutter. Exceptional C++ Style (Addison-Wesley, 2004).
* <a name="Taligent94"></a>
  \[Taligent94]: Taligent's Guide to Designing Programs (Addison-Wesley, 1994).
