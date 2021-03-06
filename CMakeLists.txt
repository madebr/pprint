cmake_minimum_required(VERSION 3.8)
project(pprint VERSION 1.0.0 LANGUAGES CXX)
option(PPRINT_BUILD_TESTS OFF)

include(GNUInstallDirs)

add_library(pprint INTERFACE)
add_library(pprint::pprint ALIAS pprint)

target_compile_features(pprint INTERFACE cxx_std_17)
target_include_directories(pprint INTERFACE
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
  $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>)

if(PPRINT_BUILD_TESTS)
  add_subdirectory(test)
endif()

install(TARGETS pprint EXPORT pprintConfig)
install(EXPORT pprintConfig
        NAMESPACE pprint::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/pprint)
install(FILES ${CMAKE_CURRENT_LIST_DIR}/include/pprint.hpp
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/pprint)
