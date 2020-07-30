set (PROJECT bson_c_lib)
project (${PROJECT})
cmake_minimum_required(VERSION 2.8.11)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Enable PIC as static libraries may be linked to shared objects
set (CMAKE_POSITION_INDEPENDENT_CODE TRUE)

# Options

# Option to build with LUA wrapper
option( BUILD_LUA "Turn on and off LUA wrapper" OFF )

# Option to build with tests
option( BUILD_TESTS "Possibility to build and run tests" OFF )

if( BUILD_LUA )
    message(STATUS "LUA wrapper is turned on")
    add_subdirectory(lua)    
endif( BUILD_LUA )
if( BUILD_TESTS )
    message(STATUS "Tests is turned on")
    add_subdirectory(test)    
endif( BUILD_TESTS )

add_subdirectory(src)
