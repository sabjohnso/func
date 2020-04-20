cmake_minimum_required(VERSION 3.12)

project(func VERSION 0.1.0 LANGUAGES C CXX)

option(func_BUILD_TESTING "Build the func tests" ON)

include(GNUInstallDirs)
set(func_INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR})
set(func_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR})
set(func_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR})
set(func_INSTALL_CONFDIR ${func_INSTALL_LIBDIR}/cmake/func-${PROJECT_VERSION})

list(INSERT CMAKE_MODULE_PATH 0 ${PROJECT_SOURCE_DIR}/cmake)
include(func_deps)

add_subdirectory(func)

if(func_BUILD_TESTING)
  include(CTest)
  if(BUILD_TESTING)
    add_subdirectory(func_testing)
  endif()
endif()

install(EXPORT func_EXPORTS
  NAMESPACE func::
  FILE func-exports.cmake
  DESTINATION ${func_INSTALL_CONFDIR})

configure_file(func-config.cmake.in func-config.cmake)
install(FILES ${PROJECT_BINARY_DIR}/func-config.cmake
  DESTINATION ${func_INSTALL_CONFDIR})








