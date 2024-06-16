cmake_minimum_required(VERSION 3.10)
project(QuantumLeapEngine)

set(CMAKE_CXX_STANDARD 17)

# Add the path to CMake modules
list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

# Find and include GLFW
find_package(glfw3 3.3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})

# Find and include GLEW
find_path(GLEW_INCLUDE_DIR NAMES GL/glew.h PATHS /opt/homebrew/include)
find_library(GLEW_LIBRARY NAMES GLEW glew PATHS /opt/homebrew/lib)
include_directories(${GLEW_INCLUDE_DIR})

# Include directories for OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIR})

# Include directories for ImGui
include_directories(${CMAKE_SOURCE_DIR}/lib/imgui)
include_directories(${CMAKE_SOURCE_DIR}/lib/imgui/backends)
file(GLOB IMGUI_SOURCES
        ${CMAKE_SOURCE_DIR}/lib/imgui/*.cpp
        ${CMAKE_SOURCE_DIR}/lib/imgui/backends/imgui_impl_glfw.cpp
        ${CMAKE_SOURCE_DIR}/lib/imgui/backends/imgui_impl_opengl3.cpp
)

# Source files
set(SOURCE_FILES main.cpp ${IMGUI_SOURCES})

# Add executable
add_executable(QuantumLeapEngine ${SOURCE_FILES})

# Link libraries
target_link_libraries(QuantumLeapEngine
        glfw
        ${GLEW_LIBRARY}
        ${OPENGL_LIBRARIES}
        "-framework GLUT"
        "-framework OpenGL"
)
