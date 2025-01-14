cmake_minimum_required(VERSION 3.12)
project(app)
set(CMAKE_MACOSX_RPATH 1)
SET(CMAKE_INSTALL_RPATH "\${ORIGIN}")

add_executable(${PROJECT_NAME} main.cpp)

find_package(SDL3 CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3)