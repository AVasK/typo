# Typo
A tiny single-header lib to get the type name in a human-readable form

![badge.cpp](https://img.shields.io/badge/C%2B%2B-14-green)
![badge.cpp](https://img.shields.io/badge/C%2B%2B-17-green)
![badge.cpp](https://img.shields.io/badge/C%2B%2B-20-green)

![badge.compiler](https://img.shields.io/badge/gcc-+-green)
![badge.compiler](https://img.shields.io/badge/clang-+-green)
![badge.compiler](https://img.shields.io/badge/msvc-+-green)
![badge.compiler](https://img.shields.io/badge/icc-+-green)

> type parsing is consteval since C++20, constexpr since C++14.

Example: 
```C++
std::cout << typo::type<T>; // should print the human-readable type name with qualifiers
```
This comes in handy in cases where you have a template function or some template metaprogramming and you're getting lost in what types are deduced :) Or sometimes you just want to print the type to the user and do so generically for any type... 

> NOTE: The implementation uses compiler-specific extensions like __PRETTY_FUNCTION__ for Clang/GCC or __FUNCSIG__ for MSVC for pre-C++20 due to the lack of a standardized way to do that. [since C++20] <source_location>'s function_name() is used which makes it even more portable across different compilers (as if there're that many C++20-compliant compilers other than GCC/Clang and MSVC though...)

> NOTE: The output is almost identical for GCC/Clang/ICC(GCC-based), but is somewhat different for MSVC, at least for now with __FUNCSIG__. But the chances are, the adoption of <source_location>'s function_name() won't change the way it's formatted but rather reuse the pre-existing compiler extension, like FUNCSIG and PRETTY_FUNCTION. So the last thing you'll want to do is to compare the "stringified" type names, since they're not fixed by any means and thus may even change unexpectedly, let alone differ between the compiler vendors. 
> In case we do need to unify the formatting, we can do some compile-time parsing of those, but this seems like an unreasonable decision since the type name is mainly used for debug purposes anyway :)

## Comparing types:
You can also write this: `type<T1> == type<T2>` instead of `std::is_same_v<T1,T2>` which I find a bit more readable and especially given that you can apply the type-modifiers to type<>: `type<T1>.remove_reference().add_const() == type<T2>` 
