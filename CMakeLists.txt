cmake_minimum_required(VERSION 3.28)

project(compies LANGUAGES CXX C)

set(CMAKE_CXX_STANDARD          20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

set(CMAKE_C_STANDARD          11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS        OFF)

set(SERIAL_DIR "${CMAKE_CURRENT_SOURCE_DIR}/serial")
set(SERIAL_SRC_DIR "${SERIAL_DIR}/src")
set(SERIAL_INC_DIR "${SERIAL_DIR}/inc")
set(SERIAL_LIB_NAME "${PROJECT_NAME}_serial")

option(BUILD_SHARED_LIBS "Build using shared libraries" OFF)

if(MSVC) 
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>")
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
    add_compile_options(/arch:AVX2) #make sure SIMD optimizations take place
endif()

file(GLOB_RECURSE SERIAL_SRCS "${SERIAL_SRC_DIR}/*.cpp")

add_library(${SERIAL_LIB_NAME} INTERFACE ${SERIAL_SRCS})
target_include_directories(${SERIAL_LIB_NAME} INTERFACE ${SERIAL_INC_DIR})
