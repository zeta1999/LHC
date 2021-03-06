cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# ---- Project ----

project(Tests CXX)

# ---- CXX Flags ----

if(NOT CMAKE_CXX_STANDARD GREATER 17)
  set(CMAKE_CXX_STANDARD 17)
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -Wextra -Werror")

# ---- Requires ----

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
  find_package(LHC REQUIRED)
endif()

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/catch2)

# ---- Create binary ----

file(GLOB tests_sources ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
add_executable(tests ${tests_sources})
target_link_libraries(tests LHC Catch2)

# ---- Add tests ----

ENABLE_TESTING() 
ADD_TEST(test tests)

