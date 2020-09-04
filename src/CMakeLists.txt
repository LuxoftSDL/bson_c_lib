cmake_minimum_required(VERSION 3.5.1)
project(bson_c_lib)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_subdirectory(emhashmap)

set(SOURCES bson_array.c bson_object.c bson_util.c)
add_library(bson SHARED ${SOURCES})
target_include_directories(bson PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(bson PUBLIC emhashmap)

set_target_properties(bson PROPERTIES PUBLIC_HEADER ${CMAKE_CURRENT_SOURCE_DIR}/bson_array.h
													 ${CMAKE_CURRENT_SOURCE_DIR}bson_object.h
													 ${CMAKE_CURRENT_SOURCE_DIR}bson_util.h)

install(TARGETS bson
		LIBRARY DESTINATION lib
        PUBLIC_HEADER DESTINATION include/bson
)

#enable_testing()  Unit tests are not compilable yet
if(CMAKE_TESTING_ENABLED)
  add_subdirectory(tests)
endif()