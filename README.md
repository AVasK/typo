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
