cmake_minimum_required(VERSION 3.22)
project(playground)

add_library(lib ${CMAKE_SOURCE_DIR}/src/file1.cpp ${CMAKE_SOURCE_DIR}/src/file2.cpp)
target_include_directories(lib PUBLIC ${CMAKE_SOURCE_DIR}/include)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "")

find_package(Doxygen)

if (DOXYGEN_FOUND)
    set(DOXYGEN_GENERATE_TREEVIEW YES)
    set(DOXYGEN_HIDE_SCOPE_NAMES YES)
    set(DOXYGEN_EXCLUDE_SYMBOLS detail)
    set(DOXYGEN_EXTRACT_ALL YES)
    set(CLANG_ASSISTED_PARSING YES)
    set(CLANG_OPTIONS "-xc++")
    set(CLANG_DATABASE_PATH ".")

    doxygen_add_docs(
        docs
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/src
    )
endif (DOXYGEN_FOUND)