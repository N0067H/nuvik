# Nuvik — Language Specification Summary

## Basic Syntax

| Item | Specification |
|---|---|
| Language Characteristics | Statically typed, natively compiled, manual memory management |
| Primitive Types | `i8~i64`, `u8~u64`, `isize`, `usize`, `f32`, `f64`, `bool`, `void` |
| Variable Declaration | `name: T = value;` |
| Mutable Variable | `mut name: T = value;` |
| Compile-Time Constant | `const name: T = value;` |
| Type Inference | Not supported |
| Initialization | Required for all variables |
| Function Declaration | `name(args): T { ... }` |
| Function Return | Final expression; no `return` keyword |
| Function Overloading | Not supported |
| Nested Functions | Not supported |
| Recursive Functions | Direct and mutual recursion supported |
| Entry Point | `main(): void`, `main(): i32`, optional `argc` and `argv` parameters |
| Conditional | `if condition { ... } else { ... }` |
| Loops | `loop`, `loop if condition` |
| Loop Control | `break`, `break value`, `continue` |
| Loop Labels | Not supported |
| Pattern Matching | `match value { pattern: expr, _: expr }` |
| `match` Types | Integers, enums, `bool` |
| `match` Exhaustiveness | Required only when used as an expression |
| `match` Default Arm | `_` must be last; duplicates prohibited |
| Multiple Patterns per Arm | Not supported |
| Empty `match` | Prohibited |
| Blocks | Independent lexical scope; final expression determines the value |
| Assignment | Statement-only; cannot be used as an expression |
| Increment/Decrement Operators | `++`, `--` not supported |
| Ternary Operator | Not supported |
| Comma Operator | Not supported |
| Comments | `//`, `/* ... */`; nested block comments not supported |

## Types and Memory

| Item | Specification |
|---|---|
| Type Casting | `expr as T` |
| Implicit Numeric Conversions | Not supported; contextual literal typing is allowed |
| Integer Overflow | Same semantics as C |
| Integer Conversions | Same semantics as C |
| Integer Literals | Decimal, hexadecimal, binary, octal; `_` separators allowed |
| Floating-Point Literals | Decimal notation, exponent notation; `_` separators allowed |
| Default Literal Types | `i32` for integers, `f64` for floating-point values |
| Logical Operators | `!`, `&&`, `\|\|`; short-circuit evaluation |
| Bitwise Operators | `&`, `\|`, `^`, `~`, `<<`, `>>`; integers only |
| Compound Assignment | `+=`, `-=`, `*=`, `/=`, `%=` and bitwise compound assignments |
| Operator Precedence | Based on C; `deref` has higher precedence than `as` |
| Pointer Types | `ptr T`, `ptr mut T` |
| Address-of Operators | `&value`, `&mut value` |
| Dereferencing | `deref p` |
| Null Pointer | `nil` |
| Pointer Arithmetic and Comparison | Based on C semantics |
| Pointer Aliasing | Allowed; no ownership or borrow checking |
| `void` Pointers | Supported; explicit `as` casting required |
| Array Type | `[T*N]` |
| Array Indexing | `array[index]`; no bounds checking |
| Array Passing | Passed by value by default; decays to a pointer in pointer contexts |
| Struct Declaration | `Name: struct { field: T; }` |
| Struct Initialization | `{ field: value }`; all fields required |
| Struct Fields | All fields of a public struct are public |
| Enum Declaration | `Name: enum T { A, B, C }` |
| Enum Conversion | Unnamed values representable by the underlying type are allowed |
| Type Alias | `Name: type = T;`; transparent alias |
| Struct and Array Comparison | Recursive value comparison; padding ignored |
| Function Pointers | `fn(T1, T2): R`; `nil` allowed |
| Strings | Null-terminated UTF-8; `ptr u8` |
| Characters | ASCII; `u8` |
| Empty Structs and Zero-Length Arrays | Prohibited |
| Partial Initialization | Prohibited |
| Size and Alignment | `sizeof T`, `alignof T` |
| Automatic Memory Management | None |

## Modules and Execution

| Item | Specification |
|---|---|
| Module Import | `name: import "path.nv";` |
| Path Resolution | Relative to the importing file's directory |
| Cyclic Imports | Compile-time error |
| Duplicate Imports | Treated as the same module |
| Access Control | Private by default; `pub` for public declarations |
| Global Variables | Supported; initializers must be constant expressions |
| Declaration Order | Top-level declarations are order-independent |
| Local Variables | Accessible only after their declaration |
| Shadowing | Allowed in nested scopes |
| Constant Expressions | Literals, operators, `const` references, `sizeof`, `alignof` |
| Function Calls in Constant Expressions | Not supported |
| `if` and `match` in Constant Expressions | Not supported |
| External Functions | `name(args): T = extern;` |
| Variadic Arguments | `...` supported only in `extern` functions |
| External ABI | C ABI |
| Memory Allocation | Uses external functions such as `malloc` and `free` |
| Evaluation Order | Left to right |
| Target Platform | Linux x86-64 |
| Compiler Implementation Language | C |
| Parser | Recursive descent parser |
| Code Generation | Direct x86-64 assembly generation |
| Assembly and Linking | External GNU tools |
| Initial IR and Optimization | None |
