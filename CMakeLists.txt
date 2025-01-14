cmake_minimum_required(VERSION 3.14)
project(${PROJECT_NAME})

# Make the executable look in its local directory for shared libs
if(Win32)
  # Windows doesn't support RPATH
elseif(APPLE)
  set(CMAKE_SKIP_BUILD_RPATH FALSE)
  set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
  set(CMAKE_MACOSX_RPATH 1)
  set(CMAKE_INSTALL_RPATH @executable_path)
elseif(UNIX)
  set(CMAKE_SKIP_BUILD_RPATH FALSE)
  set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
  set(CMAKE_INSTALL_RPATH "$\{ORIGIN\}")
endif()

add_executable(${PROJECT_NAME} main.cpp)

if(EMSCRIPTEN)
  add_subdirectory(.vendor/SDL EXCLUDE_FROM_ALL)
  # set(SDLTTF_VENDORED ON) # tell SDL_ttf to build its own dependencies
  # add_subdirectory(SDL_ttf EXCLUDE_FROM_ALL)	
else()
  find_package(SDL3 CONFIG REQUIRED)
endif()

target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3)