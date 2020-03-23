cmake_minimum_required(VERSION 3.15)
project(glfw_template)

set(CMAKE_CXX_STANDARD 14)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()
add_executable(glfw_template main.cpp include/vgl.h include/LoadShaders.h)
target_link_libraries(glfw_template ${CONAN_LIBS})
target_link_directories(glfw_template PUBLIC lib)
target_include_directories(glfw_template PUBLIC include)


