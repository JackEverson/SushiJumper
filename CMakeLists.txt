cmake_minimum_required(VERSION 3.4...4.0)

project(SushiJumper VERSION 1.0
      DESCRIPTION "A simple platformer about jumping Roundies"
      LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -WX-")
  # set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -WX-")
else()
  # set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++23")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++23")
endif()

# garden_engine
add_subdirectory(garden_engine)

#Copy Resources
add_custom_target(copy_SushiJumper_resources
COMMENT "Copying SushiJumper Resources"
)

add_custom_command(TARGET copy_SushiJumper_resources PRE_BUILD
COMMAND ${CMAKE_COMMAND} -E copy_directory_if_different
"${CMAKE_SOURCE_DIR}/res/"
"res/"
)

# Sushi application
set(SushiJumper_files
src/IntroScene.hpp
src/MainScene.cpp
src/MainGame.cpp
src/MainScene.hpp
src/Config.hpp
)

if(MSVC)
  set(APP_ICON_RESOURCE "${CMAKE_CURRENT_SOURCE_DIR}/resources.rc")
endif()

add_library(SushiJumper_lib STATIC ${SushiJumper_files})
target_include_directories(SushiJumper_lib  PUBLIC game)
target_compile_features(SushiJumper_lib PUBLIC cxx_std_23)
target_link_libraries(SushiJumper_lib PUBLIC garden_engine)

add_executable(SushiJumper src/SushiJumper.cpp ${APP_ICON_RESOURCE})
target_link_libraries(SushiJumper PUBLIC
garden_engine
SushiJumper_lib
)
add_dependencies(SushiJumper copy_SushiJumper_resources)
