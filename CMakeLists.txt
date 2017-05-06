cmake_minimum_required(VERSION 2.8.3)
project(openpose_ros)

## Add support for C++11, supported in ROS Kinetic and newer
add_definitions(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  cv_bridge
  sensor_msgs
  image_recognition_msgs
)

catkin_package()

# include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
  /home/rein/openpose/include
  /home/rein/openpose/3rdparty/caffe/include
  /home/rein/openpose/3rdparty/caffe/.build_release/src
)

add_executable(${PROJECT_NAME}_node src/openpose_ros_node.cpp)

# Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
  /home/rein/openpose/build/lib/libopenpose.so
  /home/rein/openpose/3rdparty/caffe/.build_release/lib/libcaffe.so
)
