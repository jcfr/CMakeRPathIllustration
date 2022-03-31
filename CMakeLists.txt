
cmake_minimum_required(VERSION 3.0.2)

project(CMakeRPathIllustration)

set(MY_BIN_DIR "bin")
set(MY_LIB_DIR "lib/MyWorld")

add_library(MyWorld SHARED MyWorld.cpp MyWorld.h)

set_target_properties(MyWorld PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_BIN_DIR}"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_LIB_DIR}"
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_LIB_DIR}"
  )

install(TARGETS MyWorld
  RUNTIME DESTINATION ${MY_BIN_DIR} COMPONENT RuntimeLibraries
  LIBRARY DESTINATION ${MY_LIB_DIR} COMPONENT RuntimeLibraries
  ARCHIVE DESTINATION ${MY_LIB_DIR} COMPONENT Development
  )

add_executable(myexec main.cpp)
target_link_libraries(myexec MyWorld)

set_target_properties(myexec PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_BIN_DIR}"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_LIB_DIR}"
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${MY_LIB_DIR}"
  )

install(TARGETS myexec
  RUNTIME DESTINATION ${MY_BIN_DIR} COMPONENT RuntimeLibraries
  LIBRARY DESTINATION ${MY_LIB_DIR} COMPONENT RuntimeLibraries
  ARCHIVE DESTINATION ${MY_LIB_DIR} COMPONENT Development
  )
