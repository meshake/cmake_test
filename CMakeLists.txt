cmake_minimum_required(VERSION 3.22.1)

project(MyProject VERSION 1.0
                  DESCRIPTION "My Test Project"
                  LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-m32")

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_subdirectory(math)
add_subdirectory(proto)

add_executable(MyProject math/main.cc)
target_link_libraries(MyProject math)
