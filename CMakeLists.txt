cmake_minimum_required(VERSION 2.8.3)
project(pepper_plymouth_ros)

# Find all required modules for compilation
find_package(catkin REQUIRED COMPONENTS
    roscpp
    tf
    geometry_msgs
    nav_msgs)


# Nothing that can be imported by other modules
catkin_package()


# Instructions to install launch files
install(DIRECTORY launch/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch )

# Instructions to install configuration files
install(DIRECTORY nav_conf/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/nav_conf )
install(DIRECTORY maps/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/maps )
