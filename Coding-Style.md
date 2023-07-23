We recommend to follow these guidelines when writing code for RPCS3. They aren't very strict rules since we want to be flexible and we understand that under certain circumstances some of them can be counterproductive. Just try to follow as many of them as possible:

***
### General coding style
* Variable naming: *lower_case_underscored*
    * Globals: _g__*
    * Class members: _m__*
    * Statics: _s__*
* Template parameter names: *CamelCase*, or just T, U, V...
* Avoid `#defines`, use constant variables instead.
* Put curly-brackets (`{` and `}`) on the next line.
* Try to eliminate all compiler warnings from your code.
* Try to use C++ standard data types whenever it's possible (e.g. _std::string_ instead of _QString_).
* Comment *every* hack you do, *every* snippet you comment out and *every* improvable code.
* If you have to comment or place a commented code snippet, include the reasons to do that in the comment.
* Don't use `/**/` for commenting out multiple lines. Use `//` on every line instead. In Visual Studio, for example, you can just select desired lines and use `Ctrl+K,C` combination to comment every line with `//`, `Ctrl+K,U` reverts this.
* Ensure that every source file you modify has the newline at the end of file. Every line ends with "newline" and the end of file must have "newline" too, GitHub usually warns about it.
* Use brackets around multi-term ternary operator conditions especially if they occur with other code on the same line. `(x * y) + ((a > b)? c : d)` is more readable than `x * y + a > b? c : d`.
* Use `ensure()` and `fmt::throw_exception()` in order to add asserts in your code.

***
### Emulator coding style
* Module functions and lv2 syscalls:
    * Access files converting path with `vfs::get` function.
    * Return defined error codes. That is, use `return CELL_OK;` instead of `return 0;`.
    * Prefer the type `error_code` as the return value instead of `int` or `s32`. (capable of reporting errors)
    * Use `named_thread` instead of `std::thread`. To join it, call `named_thread::operator()()`.
    * Use `g_fxo` for managing globally available variables for emulation, each variable must have a unique type.
* Use only limited number of types as function arguments and result types.
    * Use `s8`, `s16`, `s32`, `s64` for signed integral types. These are aliases to `std::int8_t`, `std::int16_t`, `std::int32_t`, `std::int64_t` respectively. `s128` has been recently added and is a 128-bit signed integer.
    * Use `u8`, `u16`, `u32`, `u64` for unsigned integral types. These are aliases to `std::uint8_t`, `std::uint16_t`, `std::uint32_t`, `std::uint64_t` respectively. `u128` has been recently added and is a 128-bit unsigned integer.
    * Use `f32` and `f64` for floating point numbers. These are aliases to `float` and `double`.
    * Use `b8` instead of `bool`. This type is a fixed 8-bit boolean-mimicking type.
    * Use `char` for UTF-8 string characters, usually as `vm::cptr<char>`. Don't treat char values as signed or unsigned numbers.
    * Function arguments and results use native endianness.
* Use `vm::ptr<>` arguments for PS3 memory pointers.
    * Pointer to the datatype `T` is `vm::ptr<T>`. For example, `void *buf` becomes `vm::ptr<void> buf`.
    * Pointer to the datatype `const T` is `vm::cptr<T>`. For example, `const char *path` becomes `vm::cptr<char> path`.
    * Pointer to the function `T(T1 arg1, ...)` is `vm::ptr<T(T1 arg1, ...)>`.
    * The function may be defined as an alias `using func_name = T(T1 arg1, ...);` and used as `vm::ptr<func_name>`.
    * Note that types `vm::ptr<u32>` and `vm::ptr<be_t<u32>>` are equal, because `be_t<>` template is implicitly applied in `vm::ptr<>` for basic types. You always work with big endian values in ps3 virtual memory, excepting some very rare cases.
    * Usual pointers (`vm::ptr`) are native-endian itself, but don't forget that dereferencing vm::ptr leads to the PS3 memory which uses big-endian values by default (if it's not known explicitly that some specific value is little-endian).
    * Pointers in PS3 memory must be big-endian: define them as `vm::bptr` or `vm::bcptr`.
* Allocate memory for temporary variables with `vm::var<>` (RAII based). It has similar semantics to `vm::ptr<>`.
    * Because it is RAII based, prefer to use it as lvalue, do not leak its freed address by doing something like: `vm::ptr<u32> _u32 = vm::var<u32>{};`
    * Use `vm::gvar<>` to allocate memory to be used globally.
* Don't forget logging at the top of every function. Print all its arguments with `%d` or `0x%x` (always use `0x%x` if not sure).
    * Don't forget `0x` in `0x%x`. It may be really confusing.
    * Use `moduleName.todo()` and other associated methods.
    * Use `.todo()` method for unimplemented functions.
    * Use `.error()` method to print error inside of function that may require user's attention. For example, some file is not found or some emulation option is not set correctly.
    * Use `.succcess()` method for well-implemeneted, rarely-called but common functions.
    * Use `.warning()` method for partially implemented functions which still have some unimplemented functionality.
    * Use `.notice()` method to print debug information unconditionally.
    * Use `.trace()` method for well implemented and often-called functions.
    * Don't return CELL_OK and other error codes if the function result type doesn't mean error code.

***
### Qt coding style
* Don't concatenate translated strings. Use `tr().arg()` instead.
