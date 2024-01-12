# CMake entry point
cmake_minimum_required (VERSION 3.0)
project (SistemaSolar)

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(GLEW REQUIRED)
find_package(Freetype REQUIRED)
#find_package(Assimp REQUIRED)

if( CMAKE_BINARY_DIR STREQUAL CMAKE_SOURCE_DIR )
  message( FATAL_ERROR "Please select another Build Directory! (and give it a clever name, like bin_Visual2012_64bits/)" )
endif()
if( CMAKE_SOURCE_DIR MATCHES " " )
  message( "Your Source Directory contains spaces. If you experience problems when compiling, this can be the cause." )
endif()
if( CMAKE_BINARY_DIR MATCHES " " )
  message( "Your Build Directory contains spaces. If you experience problems when compiling, this can be the cause." )
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include_directories(..)

set(ALL_LIBS
  ${OPENGL_LIBRARY}
  glfw
  GLEW::glew
  Freetype::Freetype
  #${ASSIMP_LIBRARIES} 
)

add_definitions(
  -DTW_STATIC
  -DTW_NO_LIB_PRAGMA
  -DTW_NO_DIRECT3D
  -DGLEW_STATIC
  -D_CRT_SECURE_NO_WARNINGS
)

add_executable(SistemaSolar
  main.cpp
  glad.c
  glad.h
  khrplatform.h
)

target_link_libraries(SistemaSolar
  ${ALL_LIBS}
)

target_link_libraries(SistemaSolar "-framework Cocoa")
target_link_libraries(SistemaSolar "-framework OpenGL")
target_link_libraries(SistemaSolar "-framework IOKit")
