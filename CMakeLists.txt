cmake_minimum_required (VERSION 2.6)
project (statismo)

ENABLE_TESTING()

SET(STATISMO_VERSION 0.9) 
SET(STATISMO_MINOR_VERSION 0)


# rpath settings
SET(CMAKE_SKIP_BUILD_RPATH  FALSE)
SET(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE) 
SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib;")
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

# Setup build locations.
if(NOT CMAKE_RUNTIME_OUTPUT_DIRECTORY)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
endif()


#
# Install boost and eigen, by just copying them from the 3rdParty directory
#  
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/3rdParty/boost DESTINATION include/)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/3rdParty/Eigen DESTINATION include/)

#
# Install the statismo and statismo itk files (these are header only, so no compilation needed)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/statismo DESTINATION include)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/statismo-config.cmake.in  ${CMAKE_CURRENT_BINARY_DIR}/statismo-config.cmake @ONLY)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/statismo-config.cmake DESTINATION lib/cmake/statismo-${STATISMO_VERSION}${STATISMO_MINOR_VERSION})


set(STATISMO_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})

