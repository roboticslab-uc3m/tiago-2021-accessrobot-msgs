cmake_minimum_required(VERSION 3.0.2)
project(accessrobot_msgs)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11 -Wno-error=shadow)

## Find packages
set(PKG_DEPS
  roscpp
  rospy
  std_msgs
)

find_package(catkin REQUIRED COMPONENTS ${PKG_DEPS})

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  control_msgs
  actionlib

  geometric_shapes
  tf2_ros
  tf2_eigen
  tf2_geometry_msgs
  tf2_msgs

  sensor_msgs

  dock_charge_sm_msgs
  laser_servoing_msgs
  move_base_msgs

  roslib
)

## Find specific system libraries
find_package(Boost REQUIRED COMPONENTS system)


################################################
## Declare ROS messages, services and actions ##
################################################
## Generate services in the 'msg' folder
add_message_files(
  FILES
  tiago_state.msg
  poi_list.msg
)

## Generate services in the 'srv' folder
#add_service_files(
#   FILES
#   GoalId.srv
#   MoveCommandSrv.srv
#   Distance3D.srv
#   TaskSrv.srv
#)

 generate_messages(
   DEPENDENCIES
   std_msgs  # Or other packages containing msgs
   geometry_msgs 
   actionlib
)

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################


###################################
## catkin specific configuration ##
###################################

catkin_package(
  INCLUDE_DIRS
#   include
  LIBRARIES 
    ${PROJECT_NAME}
  CATKIN_DEPENDS 
    ${PKG_DEPS}
  DEPENDS
    #system_lib
)

###########
## Build ##
###########

include_directories(
  include
  ${catkin_INCLUDE_DIRS}  
  accessrobot_vision
)

include_directories(SYSTEM ${EIGEN3_INCLUDE_DIRS})


####################
##  Class config  ##
####################

#add_library(${PROJECT_NAME}
#   src/navigation_manager.cpp
#   src/poi_file_handler.cpp
#   src/mod_poi_list_handler.cpp
#)

#target_link_libraries(${PROJECT_NAME}
#  ${catkin_LIBRARIES}
#)




####################
##  Demos config  ##
####################

#add_executable(navigation_test demos/navigation_test.cpp)

#add_dependencies(navigation_test ${PROJECT_NAME}_generate_messages ${catkin_EXPORTED_TARGETS})

#target_link_libraries(navigation_test
#${catkin_LIBRARIES}
#${PROJECT_NAME}
#)


######################
##  Scripts config  ##
######################


# localization
# add_executable(aruco_navigation scripts/aruco_navigation.cpp)

# add_dependencies(aruco_navigation ${catkin_EXPORTED_TARGETS})

# target_link_libraries(aruco_navigation
# ${catkin_LIBRARIES}
# ${PROJECT_NAME}
# )

# navigation node
#add_executable(navigation_node scripts/navigation_node.cpp)

#add_dependencies(navigation_node ${catkin_EXPORTED_TARGETS})

#target_link_libraries(navigation_node
#${catkin_LIBRARIES}
#${PROJECT_NAME}
#)


# mod poi list node
#add_executable(mod_poi_list_node src/mod_poi_list_node.cpp)

#add_dependencies(mod_poi_list_node ${catkin_EXPORTED_TARGETS})

#target_link_libraries(mod_poi_list_node
#${catkin_LIBRARIES}
#${PROJECT_NAME}
#)



#############
## Install ##
#############

#install(
#  TARGETS ${PROJECT_NAME}
#  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
#)

install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
)

install(DIRECTORY share/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/share
    FILES_MATCHING PATTERN "*.xml"
  )
