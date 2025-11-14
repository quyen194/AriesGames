# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.12)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project ("AriesGames" LANGUAGES C CXX)

# ========================================
# Run proto_generate.py during configure
# ========================================
find_package(Python3 REQUIRED COMPONENTS Interpreter)

execute_process(
    COMMAND ${Python3_EXECUTABLE} "${CMAKE_SOURCE_DIR}/proto_generate.py"
    WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
    RESULT_VARIABLE PROTO_RESULT
)

if(NOT PROTO_RESULT EQUAL 0)
    message(FATAL_ERROR "Proto generation failed with exit code: ${PROTO_RESULT}")
endif()

message(STATUS "Proto generation completed successfully")

# Include sub-projects.
add_subdirectory ("BomberManClient")
