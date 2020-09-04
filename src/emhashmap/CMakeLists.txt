cmake_minimum_required(VERSION 3.5.1)
project(emhashmap)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)


set(SOURCES emhashmap.c)
add_library(emhashmap SHARED ${SOURCES})
target_include_directories(emhashmap PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})


set_target_properties(emhashmap PROPERTIES PUBLIC_HEADER ${CMAKE_CURRENT_SOURCE_DIR}/emhashmap.h)

install(TARGETS emhashmap
		LIBRARY DESTINATION lib
        PUBLIC_HEADER DESTINATION include/emhashmap
)


#enable_testing()  Unit tests are not compilable yet
if(CMAKE_TESTING_ENABLED)
  add_subdirectory(tests)
endif()