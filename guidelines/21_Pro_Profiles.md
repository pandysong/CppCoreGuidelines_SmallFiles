## <a name="SS-type"></a>Pro.safety: Type-safety profile

This profile makes it easier to construct code that uses types correctly and avoids inadvertent type punning.
It does so by focusing on removing the primary sources of type violations, including unsafe uses of casts and unions.

For the purposes of this section,
type-safety is defined to be the property that a variable is not used in a way that doesn't obey the rules for the type of its definition.
Memory accessed as a type `T` should not be valid memory that actually contains an object of an unrelated type `U`.
Note that the safety is intended to be complete when combined also with [Bounds safety](21_Pro_Profiles.md#SS-bounds) and [Lifetime safety](21_Pro_Profiles.md#SS-lifetime).

An implementation of this profile shall recognize the following patterns in source code as non-conforming and issue a diagnostic.

Type safety profile summary:

* <a name="Pro-type-avoidcasts"></a>Type.1: [Avoid casts](09_ES_Expressions_and_statements.md#Res-casts):
<a name="Pro-type-reinterpretcast">a. </a>Don't use `reinterpret_cast`; A strict version of [Avoid casts](09_ES_Expressions_and_statements.md#Res-casts) and [prefer named casts](09_ES_Expressions_and_statements.md#Res-casts-named).
<a name="Pro-type-arithmeticcast">b. </a>Don't use `static_cast` for arithmetic types; A strict version of [Avoid casts](09_ES_Expressions_and_statements.md#Res-casts) and [prefer named casts](09_ES_Expressions_and_statements.md#Res-casts-named).
<a name="Pro-type-identitycast">c. </a>Don't cast between pointer types where the source type and the target type are the same; A strict version of [Avoid casts](09_ES_Expressions_and_statements.md#Res-casts).
<a name="Pro-type-implicitpointercast">d. </a>Don't cast between pointer types when the conversion could be implicit; A strict version of [Avoid casts](09_ES_Expressions_and_statements.md#Res-casts).
* <a name="Pro-type-downcast"></a>Type.2: Don't use `static_cast` to downcast:
[Use `dynamic_cast` instead](06_C_Classes_and_class_hierarchies.md#Rh-dynamic_cast).
* <a name="Pro-type-constcast"></a>Type.3: Don't use `const_cast` to cast away `const` (i.e., at all):
[Don't cast away const](09_ES_Expressions_and_statements.md#Res-casts-const).
* <a name="Pro-type-cstylecast"></a>Type.4: Don't use C-style `(T)expression` or functional `T(expression)` casts:
Prefer [construction](09_ES_Expressions_and_statements.md#Res-construct) or [named casts](#Res-cast-named).
* <a name="Pro-type-init"></a>Type.5: Don't use a variable before it has been initialized:
[always initialize](09_ES_Expressions_and_statements.md#Res-always).
* <a name="Pro-type-memberinit"></a>Type.6: Always initialize a member variable:
[always initialize](09_ES_Expressions_and_statements.md#Res-always),
possibly using [default constructors](06_C_Classes_and_class_hierarchies.md#Rc-default0) or
[default member initializers](#Rc-in-class-initializers).
* <a name="Pro-type-unon"></a>Type.7: Avoid naked union:
[Use `variant` instead](06_C_Classes_and_class_hierarchies.md#Ru-naked).
* <a name="Pro-type-varargs"></a>Type.8: Avoid varargs:
[Don't use `va_arg` arguments](05_F_Functions.md#F-varargs).

##### Impact

With the type-safety profile you can trust that every operation is applied to a valid object.
Exception may be thrown to indicate errors that cannot be detected statically (at compile time).
Note that this type-safety can be complete only if we also have [Bounds safety](21_Pro_Profiles.md#SS-bounds) and [Lifetime safety](21_Pro_Profiles.md#SS-lifetime).
Without those guarantees, a region of memory could be accessed independent of which object, objects, or parts of objects are stored in it.


## <a name="SS-bounds"></a>Pro.bounds: Bounds safety profile

This profile makes it easier to construct code that operates within the bounds of allocated blocks of memory.
It does so by focusing on removing the primary sources of bounds violations: pointer arithmetic and array indexing.
One of the core features of this profile is to restrict pointers to only refer to single objects, not arrays.

We define bounds-safety to be the property that a program does not use an object to access memory outside of the range that was allocated for it.
Bounds safety is intended to be complete only when combined with [Type safety](21_Pro_Profiles.md#SS-type) and [Lifetime safety](21_Pro_Profiles.md#SS-lifetime),
which cover other unsafe operations that allow bounds violations.

Bounds safety profile summary:

* <a href="Pro-bounds-arithmetic"></a>Bounds.1: Don't use pointer arithmetic. Use `span` instead:
[Pass pointers to single objects (only)](04_I_Interfaces.md#Ri-array) and [Keep pointer arithmetic simple](#Res-simple).
* <a href="Pro-bounds-arrayindex"></a>Bounds.2: Only index into arrays using constant expressions:
[Pass pointers to single objects (only)](04_I_Interfaces.md#Ri-array) and [Keep pointer arithmetic simple](#Res-simple).
* <a href="Pro-bounds-decay"></a>Bounds.3: No array-to-pointer decay:
[Pass pointers to single objects (only)](04_I_Interfaces.md#Ri-array) and [Keep pointer arithmetic simple](#Res-simple).
* <a href="Pro-bounds-stdlib"></a>Bounds.4: Don't use standard-library functions and types that are not bounds-checked:
[Use the standard library in a type-safe manner](17_SL_The_Standard_Library.md#Rsl-bounds).

##### Impact

Bounds safety implies that access to an object - notably arrays - does not access beyond the object's memory allocation.
This eliminates a large class of insidious and hard-to-find errors, including the (in)famous "buffer overflow" errors.
This closes security loopholes as well as a prominent source of memory corruption (when writing out of bounds).
Even an out-of-bounds access is "just a read", it can lead to invariant violations (when the accessed isn't of the assumed type)
and "mysterious values."


## <a name="SS-lifetime"></a>Pro.lifetime: Lifetime safety profile

Accessing through a pointer that doesn't point to anything is a major source of errors,
and very hard to avoid in many traditional C or C++ styles of programming.
For example, a pointer may be uninitialized, the `nullptr`, point beyond the range of an array, or to a deleted object.

See /docs folder for the initial design. The detailed formal rules are in progress (as of May 2017).

Lifetime safety profile summary:

* <a href="Pro-lifetime-invalid-deref"></a>Lifetime.1: Don't dereference a possibly invalid pointer:
[detect or avoid](09_ES_Expressions_and_statements.md#Res-deref).

##### Impact

Once completely enforced through a combination of style rules, static analysis, and library support, this profile

* eliminates one of the major sources of nasty errors in C++
* eliminates a major source of potential security violations
* improves performance by eliminating redundant "paranoia" checks
* increases confidence in correctness of code
* avoids undefined behavior by enforcing a key C++ language rule


