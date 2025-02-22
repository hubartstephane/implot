##############################################
# This file is made by shubart for chaos
##############################################

cmake_minimum_required(VERSION 3.20)
project(ImPlotLibrary)

# Options
set(CMAKE_CXX_STANDARD 11)

# make ImWchar a 32 bits value
add_compile_definitions(IMGUI_USE_WCHAR32)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add ImPlot source files
set(IMPLOT_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/implot.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/implot_items.cpp
    # Uncomment the following line to compile the ImPlot demo file if needed
    ${CMAKE_CURRENT_SOURCE_DIR}/implot_demo.cpp
)

# Add ImPlot header files
set(IMPLOT_HEADERS
    ${CMAKE_CURRENT_SOURCE_DIR}/implot.h
    ${CMAKE_CURRENT_SOURCE_DIR}/implot_internal.h
)

# Create a static library for ImPlot with its source and header files
add_library(ImPlot STATIC ${IMPLOT_SOURCES} ${IMPLOT_HEADERS})

# Include necessary directories:
# - The current directory for ImPlot headers.
# - Adjust the following path if ImGui is located elsewhere.
target_include_directories(ImPlot PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}              # ImPlot headers
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui       # ImGui headers (assumed to be in a sibling folder)
)

# Link ImPlot with ImGui.
# Make sure the ImGui target is already defined (e.g., via add_subdirectory in your workspace).
target_link_libraries(ImPlot PUBLIC ImGui)

# Install the static library
install(TARGETS ImPlot
    ARCHIVE DESTINATION lib  # For static libraries
)

# Install the header files
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
    DESTINATION include/implot
    FILES_MATCHING PATTERN "*.h"
)

# Informational message
message(STATUS "ImPlotLibrary configured and linked with ImGui")
