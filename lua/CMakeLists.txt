cmake_minimum_required(VERSION 3.5.1)
project(bson4lua)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(SOURCES bson_lua_wrapper.c )
add_library(bson4lua SHARED ${SOURCES})
target_include_directories(bson4lua PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(bson4lua PUBLIC bson)


install(TARGETS bson4lua
		LIBRARY DESTINATION lib
)