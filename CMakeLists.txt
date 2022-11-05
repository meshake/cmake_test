cmake_minimum_required(VERSION 3.22.1)

if (WIN32)
    # Set the platform on Visual Studio solution files to Win32
    # NOTE 1: this MUST be set before "project" definition
    # NOTE 2: "CACHE INTERNAL" is needed due to a bug: https://gitlab.kitware.com/cmake/cmake/-/issues/19409
    set(CMAKE_GENERATOR_PLATFORM Win32 CACHE INTERNAL "")
endif (WIN32)

project(MyProject VERSION 1.0
                  DESCRIPTION "My Test Project"
                  LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

if (UNIX)
    set(CMAKE_CXX_FLAGS "-m32")

    # Link libraries located in lib directory relative to the executables
    set(CMAKE_BUILD_WITH_INSTALL_RPATH ON)
    set(CMAKE_INSTALL_RPATH "$ORIGIN/lib")
endif (UNIX)

add_subdirectory(math)
add_subdirectory(proto)

add_executable(MyProject math/main.cc)
target_link_libraries(MyProject math)
