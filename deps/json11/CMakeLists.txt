cmake_minimum_required(VERSION 3.28...3.30)

add_library(json11 OBJECT)
add_library(OBS::json11 ALIAS json11)

target_sources(json11 PRIVATE json11.cpp PUBLIC json11.hpp)

target_include_directories(json11 PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

if(
  (CMAKE_CXX_COMPILER_ID STREQUAL AppleClang AND CMAKE_CXX_COMPILER_VERSION VERSION_GREATER_EQUAL 14)
  OR (CMAKE_CXX_COMPILER_ID STREQUAL Clang AND CMAKE_CXX_COMPILER_VERSION VERSION_GREATER_EQUAL 15)
)
  target_compile_options(json11 PUBLIC -Wno-unqualified-std-cast-call)
endif()

set_target_properties(json11 PROPERTIES FOLDER deps)
