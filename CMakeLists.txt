cmake_minimum_required(VERSION 3.10)
project(wavelib C)

set(SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# https://sodocumentation.net/cmake/topic/1443/hierarchical-project
target_include_directories(${PROJECT_NAME} PUBLIC include)

add_library(wavelib STATIC
    ${SOURCE_DIR}/conv.c
    ${SOURCE_DIR}/cwt.c
    ${SOURCE_DIR}/cwtmath.c
    ${SOURCE_DIR}/hsfft.c
    ${SOURCE_DIR}/real.c
    ${SOURCE_DIR}/wavefilt.c
    ${SOURCE_DIR}/wavefunc.c
    ${SOURCE_DIR}/wavelib.c
    ${SOURCE_DIR}/wtmath.c
    )

target_link_libraries(wavelib PUBLIC m) # link math.h

option(BUILD_AUX "Enable auxiliary" OFF)
option(BUILD_UT "Enable Unit test" OFF)
option(BUILD_TEST "Enable tests" OFF)

if(BUILD_UT)
    include(CTest)
    enable_testing()
    enable_language(CXX)
    add_subdirectory(unitTests)
endif()

if(BUILD_TEST)
    add_subdirectory(test)
    add_subdirectory(auxiliary)
endif()

if(BUILD_AUX)
    add_subdirectory(auxiliary)
endif()
