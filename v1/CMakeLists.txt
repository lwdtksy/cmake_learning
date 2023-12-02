# 这是一个CMakeLists.txt文件
cmake_minimum_required(VERSION 3.0.0)

project(APP)

set(SRC_LIST add.cpp div.cpp main.cpp mul.cpp sub.cpp)

add_executable(app ${SRC_LIST})

