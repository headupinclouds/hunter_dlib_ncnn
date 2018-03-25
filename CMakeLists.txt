cmake_minimum_required(VERSION 3.8)

option(HUNTER_KEEP_PACKAGE_SOURCES "Keep" ON)

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.28.tar.gz"
    SHA1 "8fee57e4232e35e28a88f0beafb5f2a739a3fa3c"
    LOCAL # cmake/Hunter/config.cmake
)

project(hunter_dlib_ncnn VERSION 1.0.0 LANGUAGES C CXX)

option(HDC_BUILD_NCNN "Build the ncnn test (requires opencv)" OFF)

### https://github.com/davisking/dlib/blob/master/examples/dnn_metric_learning_on_images_ex.cpp
## LICENSE: public domain. See dlib's LICENSE_FOR_EXAMPLE_PROGRAMS.txt

hunter_add_package(dlib)
find_package(dlib CONFIG REQUIRED)

add_executable(dnn_metric_learning_on_images_ex dnn_metric_learning_on_images_ex.cpp)
target_link_libraries(dnn_metric_learning_on_images_ex PUBLIC dlib::dlib)
install(TARGETS dnn_metric_learning_on_images_ex DESTINATION bin)

### https://github.com/davisking/dlib/blob/master/tools/convert_dlib_nets_to_caffe/main.cpp

add_executable(convert_dlib_nets_to_caffe convert_dlib_nets_to_caffe.cpp)
target_link_libraries(convert_dlib_nets_to_caffe PUBLIC dlib::dlib)
install(TARGETS convert_dlib_nets_to_caffe DESTINATION bin)

### https://github.com/Tencent/ncnn/blob/master/examples/squeezenet.cpp
## LICENSE: https://opensource.org/licenses/BSD-3-Clause

if(HDC_BUILD_NCC)
  hunter_add_package(ncnn)
  find_package(ncnn CONFIG REQUIRED)

  hunter_add_package(OpenCV)
  find_package(OpenCV REQUIRED)

  add_executable(squeezenet squeezenet.cpp)
  target_link_libraries(squeezenet PUBLIC ncnn::ncnn ${OpenCV_LIBS})
  install(TARGETS squeezenet DESTINATION bin)
endif()