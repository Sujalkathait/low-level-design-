cmake_minimum_required(VERSION 3.20)

project(
    CPP_ADVANCED_LOW_LEVEL_DESIGN
    VERSION 1.0.0
    DESCRIPTION "Advanced Low-Level Design (LLD) Mastery Curriculum in Modern C++"
    LANGUAGES CXX
)

# Enforce Modern C++ Standard (C++20 default, C++23 ready)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Export compile commands for language servers (clangd, clang-tidy, ccls)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Configuration Options
option(ENABLE_TESTING "Enable unit and integration test targets" OFF)
option(ENABLE_SANITIZERS "Enable Address and Undefined Behavior Sanitizers" OFF)
option(ENABLE_STRICT_WARNINGS "Treat compiler warnings as errors" OFF)

# Common Compiler Warning Flags Interface
add_library(project_warnings INTERFACE)

if(MSVC)
    target_compile_options(project_warnings INTERFACE
        /W4
        /permissive-
        /Zc:__cplusplus
        /utf-8
        $<$<BOOL:${ENABLE_STRICT_WARNINGS}>:/WX>
    )
else()
    target_compile_options(project_warnings INTERFACE
        -Wall
        -Wextra
        -Wpedantic
        -Wshadow
        -Wnon-virtual-dtor
        -Wunused
        -Woverloaded-virtual
        -Wnull-dereference
        $<$<BOOL:${ENABLE_STRICT_WARNINGS}>:-Werror>
    )
endif()

# Sanitizers Configuration (Clang / GCC)
if(ENABLE_SANITIZERS AND NOT MSVC)
    target_compile_options(project_warnings INTERFACE
        -fsanitize=address,undefined
        -fno-omit-frame-pointer
    )
    target_link_options(project_warnings INTERFACE
        -fsanitize=address,undefined
    )
endif()

# Global Include Directories
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# Helper function for adding standalone LLD executable modules
function(add_lld_target target_name source_file)
    set(full_source_path "${CMAKE_CURRENT_SOURCE_DIR}/${source_file}")
    if(EXISTS "${full_source_path}")
        add_executable(${target_name} "${full_source_path}")
        target_link_libraries(${target_name} PRIVATE project_warnings)
        set_target_properties(${target_name} PROPERTIES
            CXX_STANDARD 20
            CXX_STANDARD_REQUIRED ON
            RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
        )
    else()
        message(WARNING "Source file not found for target ${target_name}: ${full_source_path}")
    endif()
endfunction()

message(STATUS "--------------------------------------------------------")
message(STATUS " Project: ${PROJECT_NAME} (v${PROJECT_VERSION})")
message(STATUS " C++ Standard: C++${CMAKE_CXX_STANDARD}")
message(STATUS " Compiler: ${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER_VERSION}")
message(STATUS " Sanitizers Enabled: ${ENABLE_SANITIZERS}")
message(STATUS " Strict Warnings: ${ENABLE_STRICT_WARNINGS}")
message(STATUS " Testing Enabled: ${ENABLE_TESTING}")
message(STATUS "--------------------------------------------------------")

# -----------------------------------------------------------------------------
# Module Targets
# -----------------------------------------------------------------------------
# 01 - OOP Foundations
add_lld_target(lld_01_class_and_objects "01-OOP-FOUNDATIONS/01-Class-and-Objects/class_and_object.cpp")
add_lld_target(lld_02_access_modifiers "01-OOP-FOUNDATIONS/02-Access-Modifiers/access_modifiers.cpp")
