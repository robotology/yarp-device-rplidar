# SPDX-FileCopyrightText: 2006-2021 Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

yarp_prepare_plugin(rpLidar
  CATEGORY device
  TYPE RpLidar
  INCLUDE rpLidar.h
  DEFAULT ON
)

if(NOT SKIP_rpLidar)
  yarp_add_plugin(yarp_rpLidar)

  target_sources(yarp_rpLidar
    PRIVATE
      rpLidar.h
      rpLidar.cpp
  )

  target_link_libraries(yarp_rpLidar
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
  )
  list(APPEND YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS
    YARP_os
    YARP_sig
    YARP_dev
  )

  yarp_install(
    TARGETS yarp_rpLidar
    EXPORT yarp-device-rpLidar
    COMPONENT yarp-device-rpLidar
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_rpLidar PROPERTY FOLDER "Plugins/Device")
endif()
