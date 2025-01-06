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
        snprintf(buf, L, "%d", i); // only one array will be declare,
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


Convert Vector of Characters to String in C++
---------------------------------------------

https://www.geeksforgeeks.org/convert-vector-of-chars-to-string-in-cpp


std::span, std::string_view
---------------------------

[How to use std::span from C++20](https://www.cppstories.com/2023/span-cpp20)

[What are string_views and why should we use them?](https://www.sandordargo.com/blog/2022/07/13/why_to_use_string_views)


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

