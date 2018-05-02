cmake_minimum_required(VERSION 3.9)
project(cmake_sfml)

set(CMAKE_CXX_STANDARD 17)
include(ExternalProject)

set(SFML_INSTALL_LOCATION ${CMAKE_BINARY_DIR}/sfml)

ExternalProject_Add(SFML
        GIT_REPOSITORY https://github.com/SFML/SFML
        CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${SFML_INSTALL_LOCATION}
        )

include_directories(${SFML_INSTALL_LOCATION}/include)
link_directories(${SFML_INSTALL_LOCATION}/lib)

add_executable(cmake_sfml src/main.cpp)
add_dependencies(cmake_sfml SFML)
target_link_libraries(cmake_sfml
        ${SFML_INSTALL_LOCATION}/lib/libsfml-audio.so.2.4.2
        ${SFML_INSTALL_LOCATION}/lib/libsfml-graphics.so.2.4.2
        ${SFML_INSTALL_LOCATION}/lib/libsfml-window.so.2.4.2
        ${SFML_INSTALL_LOCATION}/lib/libsfml-system.so.2.4.2
        ${SFML_INSTALL_LOCATION}/lib/libsfml-network.so.2.4.2)