# The minimum version of cmake is set to 3.10. Make sure you have correctly
# installed cmake from the official sources. The cmake minimum version might
# change according to specific requirements.
cmake_minimum_required (VERSION 3.10)
project(cils LANGUAGES C CXX)

# Cmake cxx standard is set to c++-11 by default.
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O2")

# The cpp include and source directories.
set(CILS_ROOT_DIR    ${PROJECT_SOURCE_DIR})
set(CILS_INCLUDE_DIR ${CILS_ROOT_DIR}/include)
set(CILS_SOURCE_DIR  ${CILS_ROOT_DIR}/src)

# add the binary tree to the search path for include files
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${CILS_INCLUDE_DIR})

# Specify all cpp files in the source directory as sources for convenience.
file(GLOB CILS_SOURCES ${CILS_SOURCE_DIR}/*.cpp)

# Placement library.
add_library(cils SHARED
  ${CILS_SOURCES}
  )

# The binary target.
add_executable(main ${PROJECT_SOURCE_DIR}/main.cpp)
target_link_libraries(main cils)

# The install prefix is user-specified (it will be install/ dir by default
# if it is not specified explicitly).
# The cmake system will copy the include directory, the libraries and
# binaries to their destinations.
set(${CILS_INSTALL_DIR} ${PROJECT_SOURCE_DIR}/install)
set(CMAKE_INSTALL_PREFIX ${CILS_INSTALL_DIR})
install(DIRECTORY ${CILS_INCLUDE_DIR}/ DESTINATION include)
install(TARGETS cils DESTINATION lib)

# Print some important information.
message(STATUS "Host system: "                ${CMAKE_HOST_SYSTEM})
message(STATUS "System processor: "           ${CMAKE_SYSTEM_PROCESSOR})
message(STATUS "Cmake C compiler: "           ${CMAKE_C_COMPILER})
message(STATUS "Cmake CXX compiler: "         ${CMAKE_CXX_COMPILER})
message(STATUS "Cmake CXX compiler version: " ${CMAKE_CXX_COMPILER_VERSION})
message(STATUS "Cmake CXX compiler flags: "   ${CMAKE_CXX_FLAGS})
message(STATUS "Installation directory: "     ${CMAKE_INSTALL_PREFIX})

