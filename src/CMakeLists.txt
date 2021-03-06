cmake_minimum_required(VERSION 3.7)

# Project configuration
project(mnemonics LANGUAGES C)

set(SOURCES mnemonics.c dictionary.c errorcodes.c)

find_package(OpenSSL)

set(EXECUTABLE mnemonicsplay)
set(EXAMPLE_PROGRAM example)

# Executables
add_executable(${EXECUTABLE} ${SOURCES} playground.c)
target_link_libraries(${EXECUTABLE} OpenSSL::Crypto)

add_executable(${EXAMPLE_PROGRAM} ${SOURCES} example.c)
target_link_libraries(${EXAMPLE_PROGRAM} OpenSSL::Crypto)

# Compilation for GCC, Clang
if (CMAKE_C_COMPILER_ID MATCHES Clang OR ${CMAKE_C_COMPILER_ID} STREQUAL GNU)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11 -Wall -Wextra -pedantic")
endif()
