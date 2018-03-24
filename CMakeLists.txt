cmake_minimum_required(VERSION 3.8)

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.28.tar.gz"
    SHA1 "8fee57e4232e35e28a88f0beafb5f2a739a3fa3c"
    LOCAL # cmake/Hunter/config.cmake
)

project(hunter_dlib_ncnn VERSION 1.0.0 LANGUAGES C CXX)

hunter_add_package(dlib)
find_package(dlib CONFIG REQUIRED)

add_executable(dnn_metric_learning_on_images_ex dnn_metric_learning_on_images_ex.cpp)
target_link_libraries(dnn_metric_learning_on_images_ex PUBLIC dlib::dlib)
install(TARGETS dnn_metric_learning_on_images_ex DESTINATION bin)
