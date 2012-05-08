project(vtclock)
cmake_minimum_required(VERSION 2.8)

find_package(Curses REQUIRED)
include_directories(${CURSES_INCLUDE_DIRS})

include_directories("${PROJECT_BINARY_DIR}")
include_directories ("${PROJECT_SOURCE_DIR}/fonts")
include_directories ("${PROJECT_SOURCE_DIR}/msg")
add_subdirectory(msg)

add_executable(vtclock vtclock.c)
target_link_libraries (vtclock msg ${CURSES_LIBRARIES})
