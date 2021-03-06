cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

FIND_PACKAGE(OpenThreads)
FIND_PACKAGE(osg)
FIND_PACKAGE(osgUtil)
FIND_PACKAGE(osgDB)
FIND_PACKAGE(osgText)
FIND_PACKAGE(osgParticle)
FIND_PACKAGE(osgTerrain)
FIND_PACKAGE(osgViewer)
FIND_PACKAGE(osgGA)
FIND_PACKAGE(osgWidget)
FIND_PACKAGE(osgParticle)

SET(OSG_LIBS ${OPENTHREADS_LIBRARIES} ${OSG_LIBRARIES} ${OSGVIEWER_LIBRARIES} ${OSGGA_LIBRARIES} ${OSGDB_LIBRARIES} ${OSGWIDGET_LIBRARIES} ${OSGUTIL_LIBRARIES} ${OSGTEXT_LIBRARIES} ${OSGPARTICLE_LIBRARIES})

SET(POCO_FIND_REQUIRED 1)
FIND_PACKAGE(Poco)

SET(JANSSON_FIND_REQUIRED 1)
FIND_PACKAGE(jansson)

rosbuild_add_library(StimulusStarField src/StimulusStarField.cpp)
target_link_libraries(StimulusStarField ${OSG_LIBS} ${POCO_LIBRARIES} ${JANSSON_LIBRARIES} vros_display)
rosbuild_link_boost(StimulusStarField system filesystem)
