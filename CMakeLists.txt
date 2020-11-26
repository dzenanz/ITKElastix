cmake_minimum_required(VERSION 3.10.2)
project(Elastix)

if(NOT ITK_SOURCE_DIR)
  include(itk-module-init.cmake)
endif()

# When this module is loaded by an app, load Elastix too.
set(Elastix_EXPORT_CODE_INSTALL "
set(Elastix_DIR \"${elx_BINARY_DIR}\")
find_package(Elastix REQUIRED CONFIG)
include(\"${elx_BINARY_DIR}/ElastixTargets.cmake\")
")
set(Elastix_EXPORT_CODE_BUILD "
if(NOT ITK_BINARY_DIR)
  set(Elastix_DIR \"${elx_BINARY_DIR}\")
  find_package(Elastix REQUIRED CONFIG)
  include(\"${elx_BINARY_DIR}/ElastixTargets.cmake\")
endif()
")

if(NOT ITK_SOURCE_DIR)
  find_package(ITK REQUIRED)
  list(APPEND CMAKE_MODULE_PATH ${ITK_CMAKE_DIR})
  include(ITKModuleExternal)
else()
  set(ITK_DIR ${CMAKE_BINARY_DIR})
  itk_module_impl()
endif()
