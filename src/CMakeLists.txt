#
# Copyright (c) 2019-2020, University of Southampton and Contributors.
# All rights reserved.
#
# SPDX-License-Identifier: LGPL-3.0-or-later
#

file(GLOB HEADER_LIST CONFIGURE_DEPENDS "${GdbServer_SOURCE_DIR}/include/gdb-server/*.hpp")

add_library(
    gdb-server
    GdbServer.cpp
    RspConnection.cpp
    RspPacket.cpp
    Utils.cpp
    ${HEADER_LIST}
    )

target_include_directories(gdb-server
  PUBLIC $<INSTALL_INTERFACE:include> $<BUILD_INTERFACE:${GdbServer_SOURCE_DIR}/include>)

target_link_libraries(
  gdb-server
  PRIVATE
    spdlog::spdlog
  )

target_compile_features(gdb-server PUBLIC cxx_std_11)
