cmake_minimum_required(VERSION 3.20)
project(binalyzer)

# Includes. The same as -I option in gcc
include_directories(imgui)
include_directories(imgui/backends)
include_directories(nativefiledialog-extended/src/include)


# Our main script
add_executable(binalyzer src/binalyzer.cpp)

if(APPLE)
  include_directories(/Library/Frameworks/SDL2.framework/Headers)
  set(CMAKE_CXX_FLAGS "-std=c++11 -fobjc-arc -F/Library/Frameworks -framework OpenGL -framework Cocoa -framework IOKit -framework CoreVideo -framework SDL2")
  target_link_libraries(binalyzer imgui imgui_demo imgui_draw imgui_tables imgui_widgets imgui_impl_sdl imgui_impl_opengl3 nfd)
elseif(UNIX AND NOT APPLE)
  include_directories(/usr/include/SDL2)
  set(CMAKE_CXX_FLAGS "-std=c++11")
  target_link_libraries(binalyzer SDL2 GL imgui imgui_demo imgui_draw imgui_tables imgui_widgets imgui_impl_sdl imgui_impl_opengl3 nfd)
endif()

# This will compile imgui libraries
add_library(imgui imgui/imgui.cpp)
add_library(imgui_demo imgui/imgui_demo.cpp)
add_library(imgui_draw imgui/imgui_draw.cpp)
add_library(imgui_tables imgui/imgui_tables.cpp)
add_library(imgui_widgets imgui/imgui_widgets.cpp)
add_library(imgui_impl_sdl imgui/backends/imgui_impl_sdl.cpp)
add_library(imgui_impl_opengl3 imgui/backends/imgui_impl_opengl3.cpp)

add_subdirectory(nativefiledialog-extended)