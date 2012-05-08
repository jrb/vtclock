project(vtclock)
cmake_minimum_required(VERSION 2.8)

set(vtclock_VERSION_MAJOR "0")
set(vtclock_VERSION_MINOR "0")
set(vtclock_VERSION_PATCH "20120508")


set(CPACK_PACKAGE_VERSION_MAJOR ${vtclock_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${vtclock_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${vtclock_VERSION_PATCH})

find_package(Curses REQUIRED)
include_directories(${CURSES_INCLUDE_DIRS})

configure_file(
  "${PROJECT_SOURCE_DIR}/vtclock_config.h.in"
  "${PROJECT_BINARY_DIR}/vtclock_config.h"
)


include_directories("${PROJECT_BINARY_DIR}")
include_directories ("${PROJECT_SOURCE_DIR}/fonts")
include_directories ("${PROJECT_SOURCE_DIR}/msg")
add_subdirectory(msg)

add_executable(vtclock vtclock.c)
target_link_libraries (vtclock msg ${CURSES_LIBRARIES})

#CPack Config
set(CPACK_SOURCE_PACKAGE_FILE_NAME
    "${CMAKE_PROJECT_NAME}-${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH}")

set(CPACK_SOURCE_IGNORE_FILES
    "/build/;/.git/;~$;${CPACK_SOURCE_IGNORE_FILES}")
set(CPACK_SOURCE_GENERATOR "TGZ")
include(CPack)

#Because I like make dist better than make package_source
add_custom_target(dist COMMAND ${CMAKE_MAKE_PROGRAM} package_source)
