CppCoreGuidelines
-----------------

C.20: If you can avoid defining default operations, do

C.21: If you define or =delete any copy, move, or destructor function, define or =delete them all

C.67: A polymorphic class should suppress public copy/move

F.21: To return multiple “out” values, prefer returning a struct

``` C++
bool f1(const std::string& in, std::string& out1, std::string& out2)
{
    if (in.size() == 0)
        return false;
    out1 = "hello";
    out2 = "world";
    return true;
}

std::tuple<bool, std::string, std::string> f2(const std::string& in)
{
    if (in.size() == 0)
        return std::make_tuple(false, "", "");
    return std::make_tuple(true, "hello", "world");
}

struct Out
{
    std::string out1{""};
    std::string out2{""};
};

std::pair<bool, Out> f3(const std::string& in)
{
    Out o;
    if (in.size() == 0)
        return { false, o };
    o.out1 = "hello";
    o.out2 = "world";
    return { true, o };
}

std::optional<Out> f4(const std::string& in)
{
    Out o;
    if (in.size() == 0)
        return std::nullopt;
    o.out1 = "hello";
    o.out2 = "world";
    return { o };
}
```


Libraries
---------

[tanakh/cmdline: A Command Line Parser](https://github.com/tanakh/cmdline)

[jarro2783/cxxopts: Lightweight C++ command line option parser](https://github.com/jarro2783/cxxopts)

[uni-algo: Unicode Algorithms Implementation for C/C++](https://github.com/uni-algo/uni-algo)

[nemtrif/utfcpp: UTF-8 with C++ in a Portable Way](https://github.com/nemtrif/utfcpp)

[gabime/spdlog: ast C++ logging library](https://github.com/gabime/spdlog)

[renatoGarcia/icecream-cpp: 🍦Never use cout/printf to debug again](https://github.com/renatoGarcia/icecream-cpp.git)

[smasherprog/screen_capture_lite: cross platform screen/window capturing library](https://github.com/smasherprog/screen_capture_lite)
``` bash
sudo apt install libxfixes-dev
```

[serge-rgb/TinyJPEG: Single header lib for JPEG encoding. Public domain. C99. stb style.](https://github.com/serge-rgb/TinyJPEG)


What's wrong with iostream
--------------------------

[What's wrong with iostream?](https://www.reddit.com/r/cpp_questions/comments/17r9qve/whats_wrong_with_iostream)

[iostream 的用途与局限](https://www.cnblogs.com/Solstice/archive/2011/07/17/2108715.html)

**alfps**:
**{fmt}** library for formatting,
and **C FILE\* i/o** for the actual i/o except keyboard input.
For keyboard input might currently use the **Boost NoWide** library. (But there's no good solution really.)

How to print emoji with C++
---------------------------

[How to print emoji with C++](https://chriswheeler.dev/posts/how-to-print-emoji-with-cpp)

``` C++
fmt::println("🔥");
```

A Mistake
---------

``` C++

//
// Print 0 to 9
//

void f(std::string str) { printf("%s ",str.c_str()); }

int main()
{
    constexpr int N = 10;
    constexpr size_t L = 1024;

    std::vector<std::thread> thrds(N);
    for(int i = 0; i < N; ++i)
    {
        char buf[L];
        snprintf(buf, L, "%d", i); // only one array will be declared,
                                   // should use: auto buf = std::to_string(i);
        thrds[i] = std::thread(f, buf);
    }

    for(int i = 0; i < N; ++i)
        if (thrds[i].joinable())
            thrds[i].join();

    printf("\n");

    return 0;
}
```

std::thread
-----------

[C++ - compilation fails on calling overloaded function in std::thread](https://stackoverflow.com/questions/44049407/c-compilation-fails-on-calling-overloaded-function-in-stdthread)


std::condition_variable::wait
-----------------------------

[CppReference](https://en.cppreference.com/w/cpp/language/adl)

Atomically calls lock.unlock() and blocks on *this. The thread will be unblocked when notify_all() or notify_one() is executed. It may also be unblocked spuriously.
 When unblocked, calls lock.lock() (possibly blocking on the lock), then returns.


Convert Vector of Characters to String in C++
---------------------------------------------

https://www.geeksforgeeks.org/convert-vector-of-chars-to-string-in-cpp


std::span, std::string_view
---------------------------

[How to use std::span from C++20](https://www.cppstories.com/2023/span-cpp20)

[What are string_views and why should we use them?](https://www.sandordargo.com/blog/2022/07/13/why_to_use_string_views)


std::variant
------------

Typical use of [std::visit](https://en.cppreference.com/w/cpp/utility/variant/visit2)

```C++
using var_t = std::variant<int, long, double, std::string>;
 
template<class... Ts>
struct overloaded : Ts... { using Ts::operator()...; };
 
int main()
{
    std::vector<var_t> vec = {10, 15l, 1.5, "hello"};
    for (auto& v: vec)
    {
        std::visit(
            // Aggregate classes with base classes (since C++17)
            // By inheriting from these lambdas,
            // the overloaded struct can use their operator() functions.
            overloaded{ [](auto arg) { std::cout << arg << ' '; },
                        [](double arg) { std::cout << std::fixed << arg << ' '; },
                        [](const std::string& arg) { std::cout << std::quoted(arg) << ' '; } },
            v);
    }
}
```

[Aggregate initialization](https://en.cppreference.com/w/cpp/language/aggregate_initialization)


Smart Pointer
-------------

[Thread Safety of std::shared_ptr](https://www.zhihu.com/question/56836057/answer/150768793)

[Moving a unique pointer - undefined behavior on cppreference?](https://stackoverflow.com/questions/75966130/moving-a-unique-pointer-undefined-behavior-on-cppreference)


Position-independent code
-------------------------

[Wikipedia](https://en.wikipedia.org/wiki/Position-independent_code)

[Why not always use fpic (Position Independent Code)?](https://stackoverflow.com/questions/31332299/why-not-always-use-fpic-position-independent-code)


Semantic Versioning
--------------------

https://semver.org


Passing function parameters
---------------------------

[Passing function parameters correctly in C++ :: Tutorial on different references](https://www.youtube.com/watch?v=w1Cw3KFPh1A)

[Take Parameters Properly](https://www.reddit.com/r/programmingcirclejerk/comments/zmvxem/take_parameters_properly)

``` C++
void f1(std::invocable<int, double, std::string> auto&& x)
{
    x(42, 3.14, "abc");
}

void f2(void(* x)(int, double, std::string))
{
    x(42, 3.14, "abc");
}

void f3(std::move_only_function<void(int, double, std::string)>&& x)
{
    x(42, 3.14, "abc");
}

void f4(std::function<void(int, double, std::string)> x)
{
    x(42, 3.14, "abc");
}
```

The rule of three/five/zero
---------------------------

[CppReference](https://en.cppreference.com/w/cpp/language/rule_of_three)


String
------

[String literal - CppReference](https://en.cppreference.com/w/cpp/language/string_literal)

[Localization Library - CppReference](https://en.cppreference.com/w/cpp/locale)

[Generic Text Mappings](https://learn.microsoft.com/en-us/cpp/c-runtime-library/using-generic-text-mappings)

[Routine Mappings](https://learn.microsoft.com/en-us/cpp/c-runtime-library/routine-mappings)

Definitions and ODR (One Definition Rule)
-----------------------------------------

[CppReference](https://en.cppreference.com/w/cpp/language/definition)


Argument-dependent lookup
-------------------------

[CppReference](https://en.cppreference.com/w/cpp/language/adl)


std::vector
-----------

Correctly using reserve() can prevent unnecessary reallocations.


Allocator
---------

["Allocators: the Good Parts", at CppCon2017](https://github.com/phalpern/CppCon2017Code)


std::atomic
-----------

[When do I really need to use atomic<bool> instead of bool?](https://stackoverflow.com/questions/16320838/when-do-i-really-need-to-use-atomicbool-instead-of-bool)

**Pete Becker**:

There are three separate issues that "atomic" types in C++11 address:

1. tearing: a read or write involves multiple bus cycles, and a thread switch occurs in the middle of the operation; this can produce incorrect values.
2. cache coherence: a write from one thread updates its processor's cache, but does not update global memory; a read from a different thread reads global memory, and doesn't see the updated value in the other processor's cache.
3. compiler optimization: the compiler shuffles the order of reads and writes under the assumption that the values are not accessed from another thread, resulting in chaos.

Using std::atomic<bool> ensures that all three of these issues are managed correctly. Not using std::atomic<bool> leaves you guessing, with, at best, non-portable code.

[Why is integer assignment on a naturally aligned variable atomic on x86?](https://stackoverflow.com/questions/36624881/why-is-integer-assignment-on-a-naturally-aligned-variable-atomic-on-x86)


Dependency Manager
------------------

[VcPkg](https://vcpkg.io/en)
``` bash
cmake -B ./build -S . -DCMAKE_TOOLCHAIN_FILE="C:/vcpkg/scripts/buildsystems/vcpkg.cmake"
```

CPM.cmake
``` bash
mkdir -p cmake
wget -O cmake/CPM.cmake https://github.com/cpm-cmake/CPM.cmake/releases/latest/download/get_cpm.cmake
```

Conan