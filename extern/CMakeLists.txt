# SPDX-FileCopyrightText: 2006-2021 Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

# disable all warnings for current folder and subfolders
# (unless explicitly added by the user)
get_property(_USER_CMAKE_C_FLAGS CACHE CMAKE_C_FLAGS PROPERTY VALUE)
get_property(_USER_CMAKE_CXX_FLAGS CACHE CMAKE_CXX_FLAGS PROPERTY VALUE)
set(CMAKE_C_FLAGS "-w ${_USER_CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "-w ${_USER_CMAKE_CXX_FLAGS}")


# rplidar SDK
set(RPLIDAR_12_SDK_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/rplidar_12/sdk" PARENT_SCOPE)
set(RPLIDAR_20_SDK_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/rplidar_20/sdk" PARENT_SCOPE)

