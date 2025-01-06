add_library
-----------

| Type | Use Case | Produced Artifacts |
| - | - | - |
| Normal Library | Standard use, distribution, final products | Static or shared library files |
| Object Library | Intermediate builds, modular projects | Object files, not linked |
| Interface Library | Header-only libraries, managing dependencies | None (headers and compile info) |


target_link_library
-------------------

PUBLIC: Both the current target and any targets that link against it will inherit the link dependency.

PRIVATE: Only the current target will link against the specified libraries or targets, and this dependency will not be passed on to other targets.


target_compile_definitions
--------------------------

PUBLIC: Both the current target and any targets that link against it will see the compile definitions.

PRIVATE: Only the current target will use the specified compile definitions.


PkgConfig
---------

By using IMPORTED_TARGET, CMake creates a target named PkgConfig::pipewire that can use directly in your target_link_libraries command.
This ensures that all the necessary include directories, compile definitions, and libraries are correctly set up.


Others
======

``` bash
cmake -version
cmake --build /path/to/Makefile --target clean # to clear up cmake output
cmake --build /path/to/build --config Debug --target all --
```

Linking LibreOffice UNO API and Screen Capture Lite
---------------------------------------------------

``` CMake
add_library(foo SHARED main.cc)
target_link_libraries(foo
  PRIVATE
  -Wl,--allow-shlib-undefined
  -Wl,-export-dynamic
  -Wl,-z,defs
  -Wl,--no-whole-archive
  ${OO_SDK_LIBRARIES})
target_link_libraries(foo PRIVATE screencapturelite)
```
