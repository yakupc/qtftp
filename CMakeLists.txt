#
# Copyright (C) 2024 Yakup Cengiz
#

# Disable in-source builds to prevent source tree corruption.
if(" ${CMAKE_SOURCE_DIR}" STREQUAL " ${CMAKE_BINARY_DIR}")
  message(FATAL_ERROR "
FATAL: In-source builds are not allowed.
       You should create a separate directory for build files.
")
endif()

cmake_minimum_required(VERSION 3.16)

project(QtFtp LANGUAGES CXX)

# Find Qt6 packages
find_package(Qt6 REQUIRED COMPONENTS Core Network)

# Additional setup
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# ---------------------------------------------------------------------------------------
# Compiler config
# ---------------------------------------------------------------------------------------
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif()

set(CMAKE_DEBUG_POSTFIX "d")

# make sure __cplusplus is defined when using msvc and enable parallel build
if(MSVC)
  string(APPEND CMAKE_CXX_FLAGS " /Zc:__cplusplus /MP")
endif()

# Add the source directory
add_subdirectory(src)