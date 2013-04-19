cmake_minimum_required(VERSION 2.8.9)

project(CMakeRPathIllustration)

add_library(MyWorld SHARED MyWorld.cpp MyWorld.h)

set_target_properties(MyWorld PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib/MyWorld"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib/MyWorld"
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib/MyWorld"
    )
    
add_executable(myexec main.cpp)
target_link_libraries(myexec MyWorld)
