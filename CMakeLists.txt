cmake_minimum_required(VERSION 3.15)
project(glfw_template C CXX)

LINK_DIRECTORIES( ${CMAKE_SOURCE_DIR}/lib )

find_package(OpenGL REQUIRED)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

if(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup()
else()
    message(WARNING "The file conanbuildinfo.cmake doesn't exist, you have to run conan install first")
endif()


#target_include_directories(glfw_template PUBLIC include)
add_library(vgl STATIC lib/vgl.cpp include/vgl.h)
add_library(LoadShaders STATIC lib/LoadShaders.cpp include/LoadShaders.h)
target_include_directories(LoadShaders PUBLIC include)
target_include_directories(vgl PUBLIC include)
target_compile_features(LoadShaders PUBLIC cxx_std_11)
target_compile_features(vgl PUBLIC cxx_std_11)
add_executable(glfw_template main.cpp include/vgl.h include/LoadShaders.h)
target_link_libraries(glfw_template PUBLIC ${CONAN_LIBS} vgl LoadShaders)

#set_target_properties(glfw_template PROPERTIES LINKER_LANGUAGE C)
#ADD_CUSTOM_TARGET(debug ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE:STRING=Debug ${PROJECT_SOURCE_DIR})
#ADD_CUSTOM_TARGET(release ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE:STRING=Release ${PROJECT_SOURCE_DIR})