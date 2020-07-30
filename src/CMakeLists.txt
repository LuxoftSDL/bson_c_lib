project(bson)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

AUX_SOURCE_DIRECTORY(${CMAKE_CURRENT_SOURCE_DIR} source)

add_library(${PROJECT_NAME} SHARED
            ${source})
target_link_libraries(${PROJECT_NAME} emhashmap)

target_include_directories(${PROJECT_NAME} PUBLIC 
                           ${CMAKE_CURRENT_SOURCE_DIR}
                           ${CMAKE_CURRENT_SOURCE_DIR}/emhashmap)

install(
  TARGETS ${PROJECT_NAME}
  DESTINATION "${CMAKE_INSTALL_PREFIX}"
  PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
  COMPONENT bson_c_lib
)

install(
  DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
  DESTINATION "${CMAKE_INSTALL_PREFIX}"
  COMPONENT bson_c_lib FILES_MATCHING
  PATTERN "tests" EXCLUDE
  PATTERN "*.h"    
)

add_subdirectory(emhashmap)
