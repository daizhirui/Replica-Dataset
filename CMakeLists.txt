# Copyright (c) Facebook, Inc. and its affiliates. All Rights Reserved
cmake_minimum_required(VERSION 3.6.0)

project(Replica)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake/")

set(THIRD_PARTY "${CMAKE_CURRENT_LIST_DIR}/3rdparty/")

find_package(Eigen3 NO_MODULE)
if(NOT ${Eigen3_FOUND})
    message(STATUS "Using 3rd party Eigen3")
    set(Eigen_INCLUDE_DIRS "${THIRD_PARTY}/eigen")
endif()

# use system Pangolin if available
find_package(Pangolin)
if(NOT ${Pangolin_FOUND})
    message(STATUS "Using 3rd party Pangolin")
    set(Pangolin_INCLUDE_DIRS "${THIRD_PARTY}/Pangolin/build/src/include")
    list(APPEND Pangolin_INCLUDE_DIRS "${THIRD_PARTY}/Pangolin/include")
    set(Pangolin_LIBRARIES "${THIRD_PARTY}/Pangolin/build/src/libpangolin.so")
else()
    list(REMOVE_ITEM Pangolin_LIBRARIES "pango_python")
    list(REMOVE_ITEM Pangolin_LIBRARY "pango_python")
endif()

find_package(dl REQUIRED)

add_subdirectory("./ReplicaSDK")
