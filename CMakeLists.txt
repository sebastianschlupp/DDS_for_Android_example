# Copyright 2024 Sebastian Schlupp
# Copyright 2016 Proyectos y Sistemas de Mantenimiento SL (eProsima).
#
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20)

project(DDSHelloWorld)

# Find requirements
if(NOT fastcdr_FOUND)
    find_package(fastcdr 2 REQUIRED)
endif()

if(NOT fastrtps_FOUND)
    find_package(fastrtps 2.12 REQUIRED)
endif()

# Set C++11
include(CheckCXXCompilerFlag)
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_COMPILER_IS_CLANG OR
        CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    check_cxx_compiler_flag(-std=c++11 SUPPORTS_CXX11)
    if(SUPPORTS_CXX11)
        add_compile_options(-std=c++11)
    else()
        message(FATAL_ERROR "Compiler doesn't support C++11")
    endif()
endif()

message(STATUS "Configuring publisher/subscriber code...")
file(GLOB DDS_SOURCES_CXX "src/*.cxx")

# generates executable file for publisher
add_executable(publisher src/publisher.cpp ${DDS_SOURCES_CXX})
target_link_libraries(publisher fastrtps fastcdr)

# generates executable file for subscriber
add_executable(subscriber src/subscriber.cpp ${DDS_SOURCES_CXX})
target_link_libraries(subscriber fastrtps fastcdr)
