cmake_minimum_required(VERSION 2.8.3)
project(noor_bringup)

##################
## Dependencies ##
##################

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

## Find catkin macros and libraries 
find_package(catkin REQUIRED COMPONENTS
    roscpp 
    rospy 
    tf2
		tf2_ros
    nav_msgs 
    nour_msgs 
    geometry_msgs 
    sensor_msgs 
    std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES noor_bringup
  CATKIN_DEPENDS roscpp rospy tf2 tf2_ros nav_msgs nour_msgs geometry_msgs sensor_msgs std_msgs 
  DEPENDS system_lib
)

###########
## Build ##
###########

include_directories(
  include
  ${catkin_INCLUDE_DIRS}nour_msgs/
)

add_library(nour_base src/nour_base.cpp)
add_executable(nour_base_node src/nour_base_node.cpp)
target_link_libraries(nour_base_node nour_base ${catkin_LIBRARIES})
add_dependencies(nour_base nour_msgs_generate_messages_cpp)

add_executable(mpu6050_imu_converter src/imu_publisher.cpp)
target_link_libraries(mpu6050_imu_converter ${catkin_LIBRARIES})


#############
## Install ##
#############

# Future work

#############
## Testing ##
#############

# Future work