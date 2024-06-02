cmake_minimum_required(VERSION 3.0.2)
project(accessrobot_msgs)

find_package(catkin REQUIRED COMPONENTS
    message_generation std_msgs geometry_msgs)

################################################
## Declare ROS messages, services and actions ##
################################################
## Generate services in the 'msg' folder
add_message_files(
  DIRECTORY msg
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
   #actionlib
)

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################


###################################
## catkin specific configuration ##
###################################

catkin_package(
  CATKIN_DEPENDS 
  message_runtime
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")
