cmake_minimum_required(VERSION 3.3)

project(variant CXX)

include(CheckCXXCompilerFlag)

macro(add_compiler_flag testname flag)
  check_cxx_compiler_flag(${flag} ${testname})
  if (${testname})
    add_compile_options(${flag})
  endif()
endmacro()

add_library(variant INTERFACE)

target_include_directories(
  variant
  INTERFACE
  include
  )

target_compile_options(
  variant
  INTERFACE
  -std=c++14
  )

add_subdirectory(3rdparty/googletest/googletest)
include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
enable_testing()

add_subdirectory(test)
