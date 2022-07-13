cmake_minimum_required(VERSION 3.22)

# Specify the C++ language
project(cmakeTuto LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)

# Print the name of a variable and its content
function(print var)
    message("${var} = ${${var}}")
endfunction()

# Print an environment variable
function(print_env var)
    message("${var} = $ENV{${var}}")
endfunction()

# OpenGL
find_package(OpenGL REQUIRED)

# GLFW
include_directories(external/glfw/include)
add_subdirectory(external/glfw)

# ImGUI
include_directories(external/imgui external/imgui/backends)
file(GLOB_RECURSE IMGUI_SRC external/imgui/**.cpp)

# Build
add_executable(${PROJECT_NAME} src/main.cpp ${IMGUI_SRC})
target_link_libraries(${PROJECT_NAME} PRIVATE glfw ${GLFW_LIBRARIES} OpenGL::GL)
