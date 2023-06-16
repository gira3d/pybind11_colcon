cmake_minimum_required(VERSION 2.8)
project(pybind11_colcon)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

include(ExternalProject)
externalproject_add(pybind11_src
  GIT_REPOSITORY git@github.com:pybind/pybind11.git
  GIT_TAG 914c06fb25
  CONFIGURE_COMMAND cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX} ../pybind11_src
  BUILD_COMMAND make
  INSTALL_COMMAND make install
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION "include/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY cmake/
  DESTINATION "share/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.cmake"
)
