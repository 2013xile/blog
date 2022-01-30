## Variadic arguments, initializer lists and variadic templates

> There are several methods to allow a function to accept any number of extra arguments in cpp.


# Variadic arguments

The function declared as follows:

```
int printx(const char* fmt...);

int printx(const char* fmt, ...); // same as above, C compatibility
```

The values of these arguments can be accessed by the function defined in `<cstdarg>` library.

- `typedef va_list;` Declare a variable to hold the arguments.
- `void va_start( std::va_list ap, parm_n );` enables access to the variable arguments following the named argument parm_n.
- `T va_arg( std::va_list ap, T );` accesses the next variadic function argument.
- `void va_end( std::va_list ap );` cleanup for an ap object initialized by a call to va_start or va_copy.
- `void va_copy( std::va_list dest, std::va_list src );` since C++11, copies src to dest.

Example:
```
#include <iostream>
#include <cstdarg>
 
int add_nums(int count, ...) 
{
    int result = 0;
    std::va_list args;
    va_start(args, count);
    for (int i = 0; i < count; ++i) {
        result += va_arg(args, int);
    }
    va_end(args);
    return result;
}
 
int main() 
{
    std::cout << add_nums(4, 25, 25, 50, 50) << '\n';
}
```

# std::initializer_list

Defined in header `<initializer_list>`, all variable arguments are required to share a common type.

```
template< class T >
class initializer_list;
```

Example:
```
template <typename T>
void templated_fn(T) {}

int main()
{
    templated_fn<std::initializer_list<int>>({1, 2, 3}); // OK
    templated_fn<std::vector<int>>({1, 2, 3});           // also OK
}
```

# Variadic templates

A **template parameter pack** is a template parameter that accepts zero or more template arguments (non-types, types, or templates). A **function parameter pack** is a function parameter that accepts zero or more function arguments.
A template with at least one parameter pack is called a variadic template.

Example:  
Targs is the template parameter pack and Fargs is the function parameter pack.

```cpp
#include <iostream>
 
void tprintf(const char* format) // base function
{
    std::cout << format;
}
 
template<typename T, typename... Targs>
void tprintf(const char* format, T value, Targs... Fargs) // recursive variadic function
{
    for (; *format != '\0'; format++)
    {
        if (*format == '%')
        {
            std::cout << value;
            tprintf(format + 1, Fargs...); // recursive call
            return;
        }
        std::cout << *format;
    }
}
 
int main()
{
    tprintf("% world% %\n", "Hello", '!', 123);
}
```

# References
- https://en.cppreference.com/w/cpp/language/parameter_pack
- https://kheresy.wordpress.com/2017/05/05/parameter-pack-in-c11/