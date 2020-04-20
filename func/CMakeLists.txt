configure_file(config.hpp.in config.hpp)

add_library(func INTERFACE)
target_include_directories(func
  INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}>
  $<INSTALL_INTERFACE:${func_INSTALL_INCLUDEDIR}>)

add_library(func::func ALIAS func)
  
install(TARGETS func
  EXPORT func_EXPORTS
  RUNTIME DESTINATION ${func_INSTALL_BINDIR}
  LIBRARY DESTINATION ${func_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${func_INSTALL_LIBDIR})

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/config.hpp
  DESTINATION ${func_INSTALL_INCLUDEDIR})
