cmake_minimum_required(VERSION 3.2.2 FATAL_ERROR)

#include(CheckCXXCompilerFlag)
#CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
#CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
#if(COMPILER_SUPPORTS_CXX11)
#	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#elseif(COMPILER_SUPPORTS_CXX0X)
#	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
#else()
#        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
#endif()

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-std=c++11")
set(CMAKE_CXX_STANDARD_REQUIRED ON)


project(ahc)

find_package(OpenCV REQUIRED)
find_package(PCL 1.2 REQUIRED)
# Require Eigen
find_package(Eigen3 REQUIRED)


include_directories("./include")
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
include_directories(${EIGEN3_INCLUDE_DIR})

add_executable(plane_fitter ${CMAKE_SOURCE_DIR}/peac/cpp/plane_fitter.cpp)
target_link_libraries(plane_fitter ${PCL_LIBRARIES} ${OpenCV_LIBS})
install(TARGETS plane_fitter DESTINATION bin)

add_executable(plane_fitter_pcd ${CMAKE_SOURCE_DIR}/peac/cpp/plane_fitter_pcd.cpp)
target_link_libraries(plane_fitter_pcd ${PCL_LIBRARIES} ${OpenCV_LIBS})
install(TARGETS plane_fitter_pcd DESTINATION bin)
install(FILES plane_fitter_pcd.ini DESTINATION bin)

add_executable(plane_fitter_pcl_demo ${CMAKE_SOURCE_DIR}/peac/cpp/plane_fitter_pcl_demo.cpp)
target_link_libraries(plane_fitter_pcl_demo ${PCL_LIBRARIES} ${OpenCV_LIBS})
install(TARGETS plane_fitter_pcl_demo DESTINATION bin)
