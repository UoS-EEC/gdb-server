cmake_minimum_required(VERSION 3.10)

project(GdbServer
  VERSION 0.1
  DESCRIPTION "Fork from www.embecosm.com. Ported to support basic funtionality for MSP430 and CortexM0 targets, and to have clean C++ interface towards simulators."
  LANGUAGES CXX)

# If this project is not included through add_subdirectory
if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
  set(CMAKE_CXX_EXTENSIONS OFF)
endif()

find_package(spdlog REQUIRED)

add_subdirectory(src)
#add_subdirectory(apps)

# ------ Install ------
install(
  TARGETS gdb-server
  EXPORT gdb-server-targets
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  INCLUDES DESTINATION include
  )

# Include files
install(DIRECTORY include/ DESTINATION include ${CMAKE_INSTALL_INCLUDEDIR})

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/gdb-server/gdb-server-config-version.cmake"
  VERSION ${PACKAGE_VERSION}
  COMPATIBILITY AnyNewerVersion
  )

export(EXPORT gdb-server-targets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/gdb-server/gdb-server-targets.cmake"
  NAMESPACE gdb-server::
  )

configure_file(cmake/gdb-server-config.cmake
  "${CMAKE_CURRENT_BINARY_DIR}/gdb-server/gdb-server-config.cmake"
  COPYONLY)

set(ConfigPackageLocation lib/cmake/gdb-server)
install(EXPORT gdb-server-targets
  FILE
    gdb-server-targets.cmake
  NAMESPACE
    gdb-server::
  DESTINATION
    ${ConfigPackageLocation}
    )

install(
  FILES
    "${CMAKE_CURRENT_BINARY_DIR}/gdb-server/gdb-server-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/gdb-server/gdb-server-config-version.cmake"
  DESTINATION
    "${ConfigPackageLocation}"
  )
