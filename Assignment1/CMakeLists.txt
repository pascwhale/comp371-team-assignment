cmake_minimum_required(VERSION 3.10)

project(Assignment1)

include(ExternalProject)

# Set install directory
set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/dist CACHE PATH ${CMAKE_SOURCE_DIR}/dist FORCE)
if(WIN32)
    set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Debug;Release" FORCE)
endif()

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

find_package(OpenGL REQUIRED COMPONENTS OpenGL)

include(BuildGLEW)
include(BuildGLFW)
include(BuildGLM)

# Assignment1
set(EXEC assignment1)

set(SRC src/assignment1.cpp)

add_executable(${EXEC} ${SRC})

target_link_libraries(${EXEC} OpenGL::GL GLEW glfw glm)

target_include_directories(${EXEC} PUBLIC include)

list(APPEND BIN ${EXEC})
# end assignment1

# install files to install location
install(TARGETS ${BIN} DESTINATION ${CMAKE_INSTALL_PREFIX})

