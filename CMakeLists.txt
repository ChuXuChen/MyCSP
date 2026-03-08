cmake_minimum_required(VERSION 3.28)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # For Clang-Tidy
set(BUILD_SHARED_LIBS OFF) # External Library linked statically
set(CMAKE_CXX_STANDARD 23) # CPP23
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(MyCSP
        VERSION 0.1.0 # SemVer
        DESCRIPTION "A Simple Cryptographic Service Provider Based on SM"
        LANGUAGES C CXX
)

set(DEBUG_COMPILE_FLAGS
        -Wall
        -Wextra
        -Wpedantic
        -Werror
        -Wshadow
        -Wnon-virtual-dtor
        -Wold-style-cast
        -Wcast-align
        -Wunused
        -Woverloaded-virtual
        -Wconversion
        -Wsign-conversion
        -Wnull-dereference
        -Wformat=2
)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_compile_options(${DEBUG_COMPILE_FLAGS} -g)
    add_compile_options(-fsanitize=address,undefined)
    add_link_options(-fsanitize=address,undefined)
else ()
    add_compile_options(-O3 -march=native -flto)
    add_link_options(-flto)
endif ()

add_executable(mycsp main.cpp)
