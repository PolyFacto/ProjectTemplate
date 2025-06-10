cmake_minimum_required(VERSION 3.26)
project(App)

set(CMAKE_CXX_STANDARD 20)

file(GLOB_RECURSE Sources
        Source/*.cpp
)
file(GLOB_RECURSE Includes
        Include/*.h
)

add_executable(App
        ${Sources}
        ${Includes}
)

# Architecture simply replace AMD64 by x64
if(CMAKE_SYSTEM_PROCESSOR MATCHES "AMD64")
    set(ARCH_NAME "x64")
else()
    set(ARCH_NAME "${CMAKE_SYSTEM_PROCESSOR}")
endif()

# Binaries
set(BINARIES_DIR ${CMAKE_SOURCE_DIR}/Binaries/${PROJECT_NAME}/${CMAKE_BUILD_TYPE}/${CMAKE_SYSTEM_NAME}/${ARCH_NAME})
set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${BINARIES_DIR})

# Core Library
target_link_libraries(App PRIVATE Core)
target_include_directories(Core PUBLIC ${CMAKE_SOURCE_DIR}/Core/Include)