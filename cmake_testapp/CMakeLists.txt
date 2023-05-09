cmake_minimum_required(VERSION 3.23)
project(cmake_testapp)

set(CMAKE_CXX_STANDARD 17)

add_executable(cmake_testapp main.cpp general.cpp)
add_executable(cmake_testapp_calc main.cpp calc.cpp)

# add library target
# what difference of add_library and target_link_library ??
add_library(test_library STATIC calc.cpp)

# 头文件、库、将库链接到可执行文件，它们的关系是什么？？