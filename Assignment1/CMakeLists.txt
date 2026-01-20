cmake_minimum_required(VERSION 3.12)
project(Assignment1 VERSION 1.0.0 LANGUAGES CXX)

add_library(${PROJECT_NAME}_lib)

target_sources(${PROJECT_NAME}_lib PUBLIC FILE_SET HEADERS
    BASE_DIRS include
    FILES include/library.h
)

target_sources(${PROJECT_NAME}_lib PRIVATE
    src/library.cpp
)

add_executable(${PROJECT_NAME} src/main.cpp)

target_link_libraries(${PROJECT_NAME} PRIVATE ${PROJECT_NAME}_lib)

# Add the test executable
add_executable(${PROJECT_NAME}_test test/test1.cpp)

# Link tests to the main library and GTest
target_link_libraries(${PROJECT_NAME}_test PRIVATE ${PROJECT_NAME}_lib gtest_main)

# Register test
add_test(NAME ${PROJECT_NAME}_RunTests COMMAND ${PROJECT_NAME}_test)
