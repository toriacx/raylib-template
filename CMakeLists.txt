cmake_minimum_required(VERSION 3.25.1)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define source directory
set(PROJECT_SRC_DIR ${CMAKE_SOURCE_DIR}/src)

# Extract project name from the parent directory of the `CMAKE_SOURCE_DIR`
get_filename_component(PROJECT_NAME ${CMAKE_SOURCE_DIR} NAME)

project(${PROJECT_NAME})

# Define include directory
set(PROJECT_INCLUDE ${PROJECT_SRC_DIR}/include)

# Gather source files
file(GLOB PROJECT_SRC_FILES ${PROJECT_SRC_DIR}/*.cpp)

# Check if source files were found
if(NOT PROJECT_SRC_FILES)
  message(FATAL_ERROR "No source files found in ${PROJECT_SRC_DIR}")
endif()

# Load packages
find_package(raylib REQUIRED)

# Define the executable
add_executable(${PROJECT_NAME} ${PROJECT_SRC_FILES})

# Include directories
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_INCLUDE})

# Link Raylib
target_link_libraries(${PROJECT_NAME} PRIVATE raylib)

