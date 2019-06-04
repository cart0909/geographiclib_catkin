cmake_minimum_required(VERSION 2.8.3)
project(geographiclib_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)
file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)
ExternalProject_Add(geographiclib_src
  GIT_REPOSITORY https://git.code.sf.net/p/geographiclib/code
  GIT_TAG 3f750e
  CONFIGURE_COMMAND cmake ../geographiclib_src -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
  BUILD_COMMAND $(MAKE) --silent
  INSTALL_COMMAND $(MAKE) install
)

cs_install()
cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
          LIBRARIES Geographic)
