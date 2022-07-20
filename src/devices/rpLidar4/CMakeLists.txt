# SPDX-FileCopyrightText: 2006-2022 Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

yarp_prepare_plugin(rpLidar4
  CATEGORY device
  TYPE RpLidar4
  INCLUDE rpLidar4.h
  DEPENDS "TARGET YARP::YARP_math"
  DEFAULT ON)

if(NOT SKIP_rpLidar4)
  # Build rpLidar4 SDK
  if(WIN32)
    set(RPLIDAR_ARCH_DIR win32)
  elseif(APPLE)
    set(RPLIDAR_ARCH_DIR macOS)
  elseif(UNIX)
    set(RPLIDAR_ARCH_DIR linux)
  else()
    message(SEND_ERROR "rpLidar4: Unknown architecture")
  endif()

  set(RPLIDAR_SDK_SRCS
    ${RPLIDAR_20_SDK_ROOT}/src/rplidar_driver.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/sl_lidar_driver.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/sl_serial_channel.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/sl_tcp_channel.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/sl_udp_channel.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/sl_crc.cpp

    ${RPLIDAR_20_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/net_serial.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/net_socket.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/timer.cpp
    ${RPLIDAR_20_SDK_ROOT}/src/hal/thread.cpp
  )

  add_library(rpLidar4_sdk OBJECT)
  target_sources(rpLidar4_sdk PRIVATE ${RPLIDAR_SDK_SRCS})
  target_compile_options(rpLidar4_sdk PRIVATE -w)
  target_include_directories(rpLidar4_sdk
    SYSTEM PUBLIC
      ${RPLIDAR_20_SDK_ROOT}/include
      ${RPLIDAR_20_SDK_ROOT}/src
  )

  # Build YARP rpLidar4 device
  yarp_add_plugin(yarp_rpLidar4)

  target_sources(yarp_rpLidar4
    PRIVATE
      rpLidar4.h
      rpLidar4.cpp
  )
  target_compile_definitions(yarp_rpLidar4 PRIVATE _USE_MATH_DEFINES)

  target_sources(yarp_rpLidar4 PRIVATE $<TARGET_OBJECTS:rpLidar4_sdk>)
  target_include_directories(yarp_rpLidar4 SYSTEM PRIVATE $<TARGET_PROPERTY:rpLidar4_sdk,INTERFACE_INCLUDE_DIRECTORIES>)

  target_link_libraries(yarp_rpLidar4
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
      YARP::YARP_math
  )
  list(APPEND YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS
    YARP_os
    YARP_sig
    YARP_dev
    YARP_math
  )

  yarp_install(
    TARGETS yarp_rpLidar4
    EXPORT yarp-device-rpLidar4
    COMPONENT yarp-device-rpLidar4
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_rpLidar4 PROPERTY FOLDER "Plugins/Device")
endif()
