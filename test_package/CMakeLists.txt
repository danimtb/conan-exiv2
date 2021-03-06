cmake_minimum_required(VERSION 3.8)
project(Exiv2Test CXX)

set(CMAKE_CXX_STANDARD 11)
set(CXX_STANDARD_REQUIRED ON)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(KEEP_RPATHS)

if (UNIX)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra")
    set(CMAKE_BUILD_WITH_INSTALL_RPATH ON)
    if (APPLE)
        set(CMAKE_INSTALL_RPATH "@executable_path/../lib")
    else ()
        set(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")
    endif ()
endif ()

find_package(Threads REQUIRED)
find_package(Iconv)
find_package(exiv2 REQUIRED CONFIG)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_executable(testApp main.cpp)
target_link_libraries(testApp exiv2lib)
