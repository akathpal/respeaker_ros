cmake_minimum_required(VERSION 3.0.2)
project(respeaker_ros)

find_package(catkin REQUIRED COMPONENTS
  dynamic_reconfigure
)

generate_dynamic_reconfigure_options(
  cfg/Respeaker.cfg
)

catkin_package()

catkin_install_python(
  PROGRAMS
  scripts/respeaker_node.py
  scripts/speech_to_text.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY scripts launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  USE_SOURCE_PERMISSIONS
)

install(FILES requirements.txt
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

if (CATKIN_ENABLE_TESTING)
  catkin_add_nosetests(test/test_installed.py)
endif()
