cmake_minimum_required(VERSION 3.12)
project(CMakeIDL CXX)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /Fp$(IntDir)pch.pch")

include_directories(
    "${CMAKE_CURRENT_SOURCE_DIR}/"
    "${CMAKE_CURRENT_SOURCE_DIR}/Generated"
)

##########
# CMakeIDL
file(GLOB COMMON_SOURCES 
    "src/*.h" 
    "src/*.cpp"
    "src/*.idl"
    "src/*.xaml"
)


add_library(CMakeIDL SHARED 
            ${COMMON_SOURCES} 
)

set_property(TARGET CMakeIDL PROPERTY VS_WINRT_COMPONENT TRUE)
set_property(TARGET CMakeIDL PROPERTY VS_GLOBAL_ROOTNAMESPACE UwpComponentWithIDL)

set_target_properties(CMakeIDL PROPERTIES COMPILE_FLAGS "/Yupch.h")
set_source_files_properties(pch.cpp PROPERTIES COMPILE_FLAGS "/Ycpch.h")

set_target_properties(CMakeIDL PROPERTIES VS_GLOBAL_CppWinRTEnabled "true")
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT CMakeIDL)