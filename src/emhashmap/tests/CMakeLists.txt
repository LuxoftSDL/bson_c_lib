cmake_minimum_required(VERSION 3.5.1)
project(emhashmap_test)

find_package(Check REQUIRED)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(SOURCES tests.c)
add_executable(emhashmap_test  ${SOURCES})
target_link_libraries(emhashmap_test PUBLIC emhashmap check)

add_test(NAME emhashmap_test COMMAND emhashmap_test WORKING_DIRECTORY ${CMAKE_BINARY_DIR})