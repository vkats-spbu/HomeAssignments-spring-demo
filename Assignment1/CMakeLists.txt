cmake_minimum_required(VERSION 3.12)
project(Assignment1 VERSION 1.0.0 LANGUAGES CXX)

add_library(${PROJECT_NAME}_lib)
#target_include_directories(${PROJECT_NAME}_lib PUBLIC
#    $<INSTALL_INTERFACE:include>
#    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
#)
target_sources(${PROJECT_NAME}_lib PUBLIC FILE_SET HEADERS
    BASE_DIRS include
    FILES include/library.h
)

target_sources(${PROJECT_NAME}_lib PRIVATE
    src/library.cpp
)

add_executable(${PROJECT_NAME} src/main.cpp)

target_link_libraries(${PROJECT_NAME} PRIVATE ${PROJECT_NAME}_lib)
