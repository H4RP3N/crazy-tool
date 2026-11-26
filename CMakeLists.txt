cmake_minimum_required(VERSION 3.10)
project(bot C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# This gives an error with older compilers, disable dependency tracking
set(CMAKE_DISABLE_DEPENDENCY_TRACKING TRUE)
set(CMAKE_C_LINKER_DEPFILE_FLAGS "")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -fomit-frame-pointer -fdata-sections -ffunction-sections -std=c99 -static")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--gc-sections")

set(SRC_DIR src)
set(INC_DIR includes)

include_directories(${INC_DIR})
file(GLOB_RECURSE SRC_FILES "${SRC_DIR}/*.c")
file(GLOB_RECURSE HDR_FILES "${INC_DIR}/*.h")

add_executable(bot ${SRC_FILES} ${HDR_FILES})

# TODO: REMOVE THIS WHEN COMPILING NOT FOR PROXIES!
target_link_libraries(bot util)

if (DEFINED MODULES)
    add_definitions("${MODULES}")
endif()

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_definitions(-DDEBUG)
    #  add_definitions(-DKILLER)
    #add_definitions(-DTELNET_SCANNER)
    #add_definitions(-DSPEEDTEST)
endif ()
