cmake_minimum_required(VERSION 3.19.7)
include(FetchContent)
include(ExternalProject)

project(sqlite_pcre)

FetchContent_Declare(SQLite
URL      https://sqlite.org/2021/sqlite-amalgamation-3350300.zip
URL_HASH MD5=edfc21b8f1a6ea506b0a54f707634a75
)
FetchContent_MakeAvailable(SQLite)

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
ExternalProject_Add(PCRE
URL      https://ftp.pcre.org/pub/pcre/pcre2-10.36.zip
URL_HASH SHA256=3fb6d0981b6a87664810dbe625968151e42555e2983cf1c35b53a5245a5d22fc
CMAKE_ARGS -DPCRE2_STATIC_RUNTIME=ON -DPCRE2_SUPPORT_JIT=ON "-DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}/install"
)

add_library(sqlite_pcre SHARED pcre.c)
target_include_directories(sqlite_pcre PUBLIC "${sqlite_SOURCE_DIR}" "${CMAKE_BINARY_DIR}/install/include")
target_link_directories(sqlite_pcre PUBLIC "${CMAKE_BINARY_DIR}/install/lib")
target_link_libraries(sqlite_pcre "pcre2-8$<$<CONFIG:Debug>:d>")
