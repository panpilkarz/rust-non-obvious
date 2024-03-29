Random things I found non-obvious (as a C and Python dev) while learning Rust

# Fundamental types

* fixed-width numeric types built-in Rust are almost all implemented directly in modern procesors
* you can make your numbers readable this way `1_000_000_000`
* unlike C and C++, Rust treats characters as distinct from the numerical types
* there are 128-bit integeres: `u128`, `i128`

# Variables

* Rust’s char type is four bytes in size

# Memory management

* moves make source uninitialised
* tuple that holds only Copy-types, is Copy-type
* if struct holds only Copy-types, you can make it Copy-type by declaring `#[derive(Copy, Clone)]`
* `Rc` (reference count) type, unlike `Arc` (atomic reference count), is not safe to share between threads, becasue it used fast non-thread-safe code to update its reference count. Otherwise the two types are equilavent.
* use `Rc` to act kind of like Python does
* unlike in C++, Rust reference can change where it points to
* comparing refs is comparing values; to compare addresses use `std::ptr::eq`
* references can't be null; use `Option<&T>` if want to express "nullable"
* if a type implements the `Copy` trait, variables that use it do not move, but rather are trivially copied, making them still valid after assignment to another variable.
* the mechanics of passing a value to a function are similar to those when assigning a value to a variable
* if you have a mutable reference to a value, you can have no other references to that value...
* ... we also cannot have a mutable reference while we have an immutable one to the same value.

# Strings
* `String` is string type. `str` is string slice.
* having a function that takes reference to slice `fn f(s: &str)` rather than to string, will work for both strings ans slices.

# Rules of thumb

* any type that needs to do something special when a value is dropped cannot by Copy-type
* closures are lightweight function-like values
* Rust checks if code in the doc works
* `#[inline]` is a suggestion
* there is convention to name struct constructors "new"
* pattern matching requires to match all possible values. add "_" and panic() for impossible cases
* match guard is an extra condition for match
* variable names can be shadowed (ie. some variable holding int can hold String next)

# Enums
* `Option` is standard library enum with `None` and `Some`
* enums, similar to structs, can have methods and associated functions implemented
* 

# Error handling

* Rust doesn't have exceptions
* by default panic!() causes unwinding
* panic is per thread
* functions that can fail have a return type that say so `Result<Any, Error>`
* catch errors using match
* operator ? propagates error to the caller stack frame
* to handle errors in main use `.except()`

# Expressions

* most of the control flow tools in C are statements. In Rust they are all expressions.
* if an match can produce values
* for loop follows move-semantic and consumes the values it iterates. to avoid this, iterate over references.
* loop can return; break has argument
* loop can be labelled with lifetime and break can exists the outer loop
* divergent functions (->!) never exits

# Crates

* Rust compiles crates into .rlib files
* you should specify edition yhou code is using. 2015 is default
* `use std::fs::{self, File}` imports `both std::fs` and `std::fs::File`

