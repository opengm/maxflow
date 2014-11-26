# default build-type (release)
IF(DEFINED CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ELSE()
   SET(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ENDIF()

# check cmake version
cmake_minimum_required(VERSION 2.8)

# project name
project (maxflow)

# set output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

# set source files
SET(MAXFLOW_SRC_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/graph.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/maxflow.cpp
)

# create library
add_library (maxflow ${MAXFLOW_SRC_FILES})
add_library (maxflow-shared SHARED ${MAXFLOW_SRC_FILES})

# point to include directory
target_include_directories (maxflow PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_include_directories (maxflow-shared PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

# install
if(NOT DEFINED MAXFLOW_INSTALL_LIB_DESTINATION)
   set(MAXFLOW_INSTALL_LIB_DESTINATION lib)
endif(NOT DEFINED MAXFLOW_INSTALL_LIB_DESTINATION)
if(NOT DEFINED MAXFLOW_INSTALL_HEADER_DESTINATION)
   set(MAXFLOW_INSTALL_HEADER_DESTINATION include)
endif(NOT DEFINED MAXFLOW_INSTALL_HEADER_DESTINATION)

install(TARGETS maxflow DESTINATION ${MAXFLOW_INSTALL_LIB_DESTINATION})
install(TARGETS maxflow-shared DESTINATION ${MAXFLOW_INSTALL_LIB_DESTINATION})
install(DIRECTORY include/maxflow DESTINATION ${MAXFLOW_INSTALL_HEADER_DESTINATION})