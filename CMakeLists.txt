﻿# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project(wxApp VERSION 0.1.3 LANGUAGES CXX)

# Include sub-projects.
add_subdirectory ("wxApp")
