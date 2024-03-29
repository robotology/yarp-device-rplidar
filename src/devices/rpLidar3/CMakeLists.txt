# SPDX-FileCopyrightText: 2006-2021 Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

yarp_prepare_plugin(rpLidar3
  CATEGORY device
  TYPE RpLidar3
  INCLUDE rpLidar3.h
  DEPENDS "TARGET YARP::YARP_math"
  DEFAULT ON)

if(NOT SKIP_rpLidar3)
  # Build rpLidar3 SDK
  if(WIN32)
    set(RPLIDAR_ARCH_DIR win32)
  elseif(APPLE)
    set(RPLIDAR_ARCH_DIR macOS)
  elseif(UNIX)
    set(RPLIDAR_ARCH_DIR linux)
  else()
    message(SEND_ERROR "rpLidar3: Unknown architecture")
  endif()

  set(RPLIDAR_SDK_SRCS
    ${RPLIDAR_12_SDK_ROOT}/src/rplidar_driver.cpp
    ${RPLIDAR_12_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/net_serial.cpp
    ${RPLIDAR_12_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/net_socket.cpp
    ${RPLIDAR_12_SDK_ROOT}/src/arch/${RPLIDAR_ARCH_DIR}/timer.cpp
    ${RPLIDAR_12_SDK_ROOT}/src/hal/thread.cpp
  )

  add_library(rpLidar3_sdk OBJECT)
  target_sources(rpLidar3_sdk PRIVATE ${RPLIDAR_SDK_SRCS})
  target_compile_options(rpLidar3_sdk PRIVATE -w)
  target_include_directories(rpLidar3_sdk
    SYSTEM PUBLIC
      ${RPLIDAR_12_SDK_ROOT}/include
      ${RPLIDAR_12_SDK_ROOT}/src
  )

  # Build YARP rpLidar3 device
  yarp_add_plugin(yarp_rpLidar3)

  target_sources(yarp_rpLidar3
    PRIVATE
      rpLidar3.h
      rpLidar3.cpp
  )
  target_compile_definitions(yarp_rpLidar3 PRIVATE _USE_MATH_DEFINES)

  target_sources(yarp_rpLidar3 PRIVATE $<TARGET_OBJECTS:rpLidar3_sdk>)
  target_include_directories(yarp_rpLidar3 SYSTEM PRIVATE $<TARGET_PROPERTY:rpLidar3_sdk,INTERFACE_INCLUDE_DIRECTORIES>)

  target_link_libraries(yarp_rpLidar3
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
    TARGETS yarp_rpLidar3
    EXPORT yarp-device-rpLidar3
    COMPONENT yarp-device-rpLidar3
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_rpLidar3 PROPERTY FOLDER "Plugins/Device")
endif()
