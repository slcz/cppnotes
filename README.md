# cppnotes
## Build system, package manager
Use cmake + hunter.
- [Hunter new package list](https://docs.hunter.sh/en/latest/packages.html)
- Below is a minumum modern Cmake template.
```
cmake_minimum_required (VERSION 3.8)
include("HunterGate.cmake")
HunterGate(
        URL "https://github.com/ruslo/hunter/archive/v0.18.12.tar.gz"
        SHA1 "7e8c74787e08c476484d3e5106524fe7a5a0cc56"
)
project (foo VERSION 1.0 LANGUAGES CXX)
hunter_add_package(Boost COMPONENTS program_options)
find_package(Boost CONFIG REQUIRED program_options)
add_executable(foo main.c++ foo1.c++ foo2.c++)
# target_include_directories(foo, "src")
target_compile_options(foo PRIVATE "-Wall" "-Werror" "-O2" "-g")
# use meta-features cxx_std_17
target_compile_features(foo PRIVATE cxx_std_17)
target_include_directories(foo PRIVATE "src")
target_link_libraries(foo PRIVATE Boost::program_options)
```
