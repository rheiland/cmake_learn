cmake_minimum_required (VERSION 3.5)
# actually, I have no idea what min version is req'd

# put before COMPILER so we can subsitute compiler on command line.
project (PhysiCell)

FIND_PACKAGE (OpenMP)

#OPTION(BUILD_SHARED_LIBS "Build shared libraries" ON)

#if (OPENMP_FOUND)
#    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
#    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
#endif()

# These will be default compilers, but can substitute others on command line.
# e.g., if creating in ./build dir:
# <path>/build$ cmake -DCMAKE_CXX_COMPILER=g++-7 -DCMAKE_C_COMPILER=gcc-7 ..
set (CMAKE_C_COMPILER gcc)
set (CMAKE_CXX_COMPILER g++)

# in original Makefile, we specified:
#set (CMAKE_CXX_FLAGS "-march=native -O3 -fomit-frame-pointer -mfpmath=both -fopenmp -m64 -std=c++11")

set (CMAKE_CXX_STANDARD 11)
# Not sure about this.
#set (CMAKE_CXX_STANDARD_REQUIRED ON)


# rf. https://cmake.org/cmake/help/v3.0/variable/CMAKE_VERSION.html
set (PhysiCell_VERSION_MAJOR 1)
set (PhysiCell_VERSION_MINOR 2)
set (PhysiCell_VERSION_PATCH 1)

# should we use our own math functions
#option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file (
  "${PROJECT_SOURCE_DIR}/PhysiCellConfig.h.in"
  "${PROJECT_BINARY_DIR}/PhysiCellConfig.h"
  )

# add the binary tree to the search path for include files
# so that we will find PhysiCellConfig.h
include_directories ("${PROJECT_BINARY_DIR}")

include_directories ("${PROJECT_SOURCE_DIR}/BioFVM")
add_subdirectory (BioFVM)
include_directories ("${PROJECT_SOURCE_DIR}/core")
add_subdirectory (core)
include_directories ("${PROJECT_SOURCE_DIR}/modules")
add_subdirectory (modules)
include_directories ("${PROJECT_SOURCE_DIR}/custom_modules")
add_subdirectory (custom_modules)

set (EXTRA_LIBS ${EXTRA_LIBS} BioFVMFunctions CoreFunctions ModulesFunctions CustomModulesFunctions)

# add the executable
add_executable (PhysiCell main.cpp)
target_link_libraries (PhysiCell  ${EXTRA_LIBS})
