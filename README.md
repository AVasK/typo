# Typo
A tiny single-header lib to get the type name in a human-readable form

> Tested with recent enough versions of
- GCC
- Clang
- MSVC
- ICC

> type parsing is consteval since C++20, constexpr since C++14.

Example: 
```C++
std::cout << typo::type<T>; // should print the human-readable type name with qualifiers
```

> Uses __PRETTY_FUNCTION__, __FUNCSIG__ or <source_location>'s function_name() which makes it even more portable since C++20.


## Comparing types:
You can also write this: `type<T1> == type<T2>` instead of `std::is_same_v<T1,T2>` which I find a bit more readable and especially given that you can apply the type-modifiers to type<>: `type<T1>.remove_reference().add_const() == type<T2>` 
