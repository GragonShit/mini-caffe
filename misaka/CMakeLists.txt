project(Misaka)
cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

# change default build type from Debug to Release if not set
if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type specified; defaulting to CMAKE_BUILD_TYPE=Release.")
    set(CMAKE_BUILD_TYPE Release CACHE STRING
        "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
        FORCE)
else(NOT CMAKE_BUILD_TYPE)
    if(CMAKE_BUILD_TYPE STREQUAL "Debug")
        message("==========================================================================================")
        message(STATUS "Build type: Debug. Performance will be terrible!")
        message(STATUS "Add -DCMAKE_BUILD_TYPE=Release to the CMake command line to get an optimized build.")
        message("==========================================================================================")
    endif(CMAKE_BUILD_TYPE STREQUAL "Debug")
endif(NOT CMAKE_BUILD_TYPE)

# use C++11 by default
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
message(STATUS "C++11 support has been enabled by default.")

# include directories
include_directories(${CMAKE_SOURCE_DIR}/dlpack/include)
include_directories(${CMAKE_SOURCE_DIR}/include)

# setup source files
file(GLOB MISAKA_INCLUDE ${CMAKE_SOURCE_DIR}/include/misaka/*.h)
file(GLOB MISAKA_SOURCE ${CMAKE_SOURCE_DIR}/src/*.cc)

source_group(include FILES ${MISAKA_INCLUDE})
source_group(src FILES ${MISAKA_SOURCE})

add_executable(misaka ${MISAKA_INCLUDE} ${MISAKA_SOURCE})
