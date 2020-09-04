cmake_minimum_required(VERSION 3.5.1)
project(bson)


add_subdirectory(src)
add_subdirectory(lua)

#enable_testing()  Unit tests are not compilable yet
if(CMAKE_TESTING_ENABLED)
  add_subdirectory(tests)
endif()