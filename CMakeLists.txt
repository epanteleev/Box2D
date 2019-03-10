cmake_minimum_required(VERSION 2.8)

# Specify default build type if none provided
if(NOT CMAKE_BUILD_TYPE)
	set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build (Debug or Release)" FORCE)
endif()

project(Box2d)

set(BOX2D_VERSION 2.3.2)

option(BOX2D_INSTALL_DOC      "Install Box2D documentation" OFF)
option(BOX2D_INSTALL_EXAMPLES "Install Box2D examples" OFF)
option(BOX2D_BUILD_SHARED     "Build Box2D shared libraries" ON)
option(BOX2D_BUILD_EXAMPLES   "Build Box2D examples" ON)

# The Box2D library.
add_subdirectory(box2d)
if(BOX2D_BUILD_EXAMPLES)
    find_package(OpenGL REQUIRED)
    add_subdirectory(Testbed)
endif()
