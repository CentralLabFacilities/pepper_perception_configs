### Maintainer: flier[@techfak.uni-bielefeld.de] ###
cmake_minimum_required(VERSION 2.8)
PROJECT(pepper_perception_configs)
SET(CMAKE_BUILD_TYPE distribution)

MESSAGE("-- You are building on: ${CMAKE_SYSTEM_NAME}")
MESSAGE("-- If you don't set -DCMAKE_INSTALL_PREFIX, defaults are used.")

SET(PREFIX "/usr/local")
IF (CMAKE_INSTALL_PREFIX)
    SET(PREFIX ${CMAKE_INSTALL_PREFIX})
    MESSAGE("-- Found install PREFIX: " ${PREFIX})
ENDIF()

FILE(GLOB yaml_files "vision/clf_perception/*.yaml.in")

# Replace the @PREFIX@
FOREACH(file ${yaml_files})
    STRING(REGEX REPLACE "^(.*)\\.in$" "\\1" demofile ${file})
    CONFIGURE_FILE(${file} "${CMAKE_CURRENT_BINARY_DIR}/${demofile}" @ONLY)
    INSTALL(FILES "${CMAKE_CURRENT_BINARY_DIR}/${demofile}" DESTINATION "${PREFIX}/share/${CMAKE_PROJECT_NAME}/vision/clf_perception")
ENDFOREACH()

INSTALL(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/vision" DESTINATION ${PREFIX}/share/${CMAKE_PROJECT_NAME})