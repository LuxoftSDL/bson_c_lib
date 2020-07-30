project(bson4lua)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

AUX_SOURCE_DIRECTORY(${CMAKE_CURRENT_SOURCE_DIR} source)

# Append directories in the linker search path and outside the project
set (CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

find_package(Lua 5.2 EXACT REQUIRED)

list(GET LUA_LIBRARIES 0 LUA_LIB)
list(GET LUA_LIBRARIES 1 LIBM_LIB)

message(STATUS "lualib : ${LUA_LIB}")
message(STATUS "libmlib : ${LIBM_LIB}")

add_library(lua::lua UNKNOWN IMPORTED GLOBAL)
set_target_properties(lua::lua
  PROPERTIES
    INTERFACE_INCLUDE_DIRECTORIES "${LUA_INCLUDE_DIR}"
    IMPORTED_LOCATION ${LUA_LIB}
    IMPORTED_LINK_DEPENDENT_LIBRARIES ${LIBM_LIB}
)

set(LIBRARIES
  lua::lua  
  bson  
)

add_library(${PROJECT_NAME} SHARED
            ${source})
target_link_libraries(${PROJECT_NAME} ${LIBRARIES})

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

install(
  TARGETS ${PROJECT_NAME}
  DESTINATION "${CMAKE_INSTALL_PREFIX}"
  PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
  COMPONENT bson_c_lib)
