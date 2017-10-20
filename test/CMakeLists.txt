cmake_minimum_required(VERSION 2.8)

include(ExternalProject)


set(DEPEND_LIB_ROOT ${CMAKE_CURRENT_BINARY_DIR}/Depends)

ExternalProject_Add(
  ### Target name
  GoogleTest
  ### Path to Git repository
  GIT_REPOSITORY https://github.com/google/googletest.git
  ### Specify TAG
  GIT_TAG release-1.8.0
  ### Path to source tree
  SOURCE_DIR ${DEPEND_LIB_ROOT}/src/googletest
  PREFIX ${CMAKE_CURRENT_BINARY_DIR}/lib
  BINARY_DIR ${DEPEND_LIB_ROOT}/build/googletest
  INSTALL_COMMAND ""
)


ExternalProject_Get_Property(GoogleTest source_dir)
include_directories(${source_dir}/include)

ExternalProject_Get_Property(GoogleTest binary_dir)
add_library(gtest STATIC IMPORTED)
set_property(
    TARGET gtest
    PROPERTY IMPORTED_LOCATION ${binary_dir}/libgtest.lib
    )
add_library(gtest_main STATIC IMPORTED)
set_property(
    TARGET gtest_main
    PROPERTY IMPORTED_LOCATION ${binary_dir}/libgtest_main.lib
    )