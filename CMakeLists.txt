
cmake_minimum_required(VERSION 3.12)
project(MyAwesomeProject VERSION 1.0.0 LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

#Setup modern-tyle googletest
include(CTest)
include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest
  GIT_TAG v1.17.0
)
FetchContent_MakeAvailable(googletest)

# Automate astyle application
find_program(ASTYLE_EXECUTABLE astyle DOC "A tool to format the code")

# Add a custom target
add_custom_target("format" COMMAND
  "${ASTYLE_EXECUTABLE}"
  -r --options=${CMAKE_CURRENT_SOURCE_DIR}/astyle.ini
   ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
   ${CMAKE_CURRENT_SOURCE_DIR}/*.h
  VERBATIM
)

# Add subdirectories for assignments
add_subdirectory(Assignment1)

