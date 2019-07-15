cmake_minimum_required(VERSION 2.8)
project(FS)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -march=native -Wno-narrowing -std=c++0x -fPIC -DNDEBUG  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -march=native -Wno-narrowing -std=c++0x -fPIC -DNDEBUG  -O3 -march=native")


#message("${PROJECT_SOURCE_DIR}")

#include_directories(${PROJECT_SOURCE_DIR}/include
#        ${PROJECT_SOURCE_DIR}
#        ${PROJECT_SOURCE_DIR}/3rd/cxxopts/include
#        ${PROJECT_SOURCE_DIR}/3rd/Simd/src
#        )

include(${PROJECT_SOURCE_DIR}/cmake/opencv.cmake)




file(GLOB FS_HEADERS "faceswapper/*.h")
file(GLOB FS_SRC     "faceswapper/*.cpp")
add_library(${PROJECT_NAME} STATIC ${FS_SRC}  ${FS_HEADERS})


message(" ${OPENCV3_LIBS}")
add_dependencies(${PROJECT_NAME} opencv)
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} gcc -ldl -lz -lpthread)

add_executable(demo ${PROJECT_SOURCE_DIR}/test/main.cpp)
target_link_libraries(demo ${PROJECT_NAME} ${OpenCV_LIBS})