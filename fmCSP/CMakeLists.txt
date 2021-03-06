cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

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

rosbuild_add_boost_directories()


rosbuild_add_executable(serial_string src/Serial_Port/serial_string/serial_string.cpp)
rosbuild_add_executable(serial_string src/Serial_Port/serial_string/serialInterface.cpp)
rosbuild_link_boost(serial_string system)

rosbuild_add_executable(serial_binary src/Serial_Port/serial_binary/serial_binary.cpp)
rosbuild_add_executable(serial_binary src/Serial_Port/serial_binary/serial_binary_interface.cpp)
rosbuild_link_boost(serial_binary system)


IF(EXISTS /usr/include/can4linux.h)
rosbuild_add_executable(can_can4linux src/CAN_bus/can_can4linux/can_can4linux.cpp)
ENDIF(EXISTS /usr/include/can4linux.h)

rosbuild_add_executable(can_socketcan src/CAN_bus/can_socketcan/can_socketcan.cpp)
rosbuild_add_executable(can_socketcan src/CAN_bus/can_socketcan/SocketCan.cpp)
rosbuild_link_boost(can_socketcan system thread)

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})
