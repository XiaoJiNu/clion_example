#set(Boost_USE_STATIC_LIBS OFF) #enable dynamic linking
#
## see https://cmake.org/cmake/help/latest/module/FindBoost.html
#find_package(Boost REQUIRED COMPONENTS unit_test_framework)
#c
#include_directories(${Boost_INCLUDE_DIR})
#
## create a cmake_testapp_boost target from test.cpp
#add_executable(cmake_testapp_boost tests.cpp)
#
## Note: a target should be already defined using 'add_executable' or 'add_library'
#target_link_libraries(cmake_testapp_boost ${Boost_LIBRARIES})
#
## link Boost with code library
#target_link_libraries(cmake_testapp_boost test_library)


set(Boost_USE_STATIC_LIBS OFF) #enable dynamic linking

# search for unit_test_framework
find_package(Boost REQUIRED COMPONENTS unit_test_framework)

include_directories(${Boost_INCLUDE_DIR})

# create a cmake_testapp_boost target from test.cpp
add_executable(cmake_testapp_boost tests.cpp)

# link Boost libraries to the new target
target_link_libraries(cmake_testapp_boost ${Boost_LIBRARIES})

# link Boost with code library
target_link_libraries(cmake_testapp_boost test_library)

# Q1. find_package() ??
