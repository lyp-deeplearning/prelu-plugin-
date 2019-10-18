cmake_minimum_required(VERSION 2.8)
project(main)

add_definitions(-std=c++11)
#set(QMAKE_CXXFLAGS "-std=c++11")
SET(PATH_CU_FILES /home/lyp/project/tf_insightface/TensorRT-Prelu-master)
FILE(GLOB_RECURSE CU_LIST ${PATH_CU_FILES}/*.cu)
set(OpenCV_DIR /home/lyp/software/openvino/opencv/cmake)

find_package(OpenCV REQUIRED)
find_package(CUDA REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(/usr/include/x86_64-linux-gnu)

#add plugin define
include_directories(/home/lyp/project/tf_insightface/TensorRT-Prelu-master)


link_directories(/usr/local/cuda-9.0/targets/x86_64-linux/lib)
link_directories( /usr/lib/x86_64-linux-gnu)



#/usr/local/cuda-9.0/targets/x86_64-linux/lib/libcudart.so.9.0.176
AUX_SOURCE_DIRECTORY(./ DIR_SRCS)
#add_executable( main  serialize.cpp Gplugin.cpp GpluginGPU.cu)
cuda_add_executable(main  main.cpp Gplugin.cpp GpluginGPU.cu)
set(CMAKE_CXX_FLAGS  "-lpthread")
set(CMAKE_CXX_FLAGS  "-O3")
target_link_libraries( main ${OpenCV_LIBS} )
#target_link_libraries( main openblas)
target_link_libraries( main cudart)
target_link_libraries( main nvinfer)
target_link_libraries( main nvparsers)
target_link_libraries( main nvonnxparser)
target_link_libraries( main nvcaffe_parser)
#target_link_libraries( main opencv_world)

