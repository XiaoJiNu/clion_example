cmake_minimum_required(VERSION 3.23)
project(cmake_testapp)

set(CMAKE_CXX_STANDARD 17)

# 3. Adding files to targets
# what dose add_executable(cmake_testapp main.cpp) do ??
# The add_executable(cmake_testapp main.cpp) command is used in a CMakeLists.txt file to define
# an executable target named cmake_testapp. This command tells CMake to compile the main.cpp source file
# and generate an executable binary named cmake_testapp.
#
# In summary, add_executable(cmake_testapp main.cpp) creates an executable target with the specified name
# and source file, which will be built when the CMake project is built.
# 这个函数是什么，功能是什么(用来干什么)，如何使用，举例
add_executable(cmake_testapp main.cpp)

# 4. Adding(Create) targets and reloading the project
add_executable(cmake_testapp_calc main.cpp calc.cpp)

# add library target
add_library(test_library STATIC calc.cpp)

# 5. CMake presets and CLion CMake profiles
# 6. Build types

# 7. Adding include directories，指定target文件的一些头文件搜索路经
# 头文件、库、将库链接到可执行文件，它们的关系是什么？？
# target_include_directories和include_directories关系是什么？？
# target_include_directories()是让target文件cmake_testapp_calc中的源文件可以使用includes/math和includes/general中的头文件
#target_include_directories(cmake_testapp_calc PUBLIC includes/math)
#target_include_directories(cmake_testapp_calc PUBLIC includes/general)
include_directories(includes/math)
include_directories(includes/general)

# 8. Linking libraries
# 找到test_library 或者lib的路经，将这个路经赋值给TEST_LIBRARY
find_library(TEST_LIBRARY test_library lib)
# 将TEST_LIBRARY路径中的库链接到cmake_testapp目标文件，
# the target_link_libraries command is used to link the cmake_testapp target with the library
# specified in the ${TEST_LIBRARY} variable. The LINK_PUBLIC option specifies
# that the library should be linked as a public dependency of the target.
target_link_libraries(cmake_testapp LINK_PUBLIC ${TEST_LIBRARY})

# add_subdirectory()指定的目录中需要有自己的CMakeLists.txt
# 2023.05.13 TODO
add_subdirectory(test)


# 11. Working with CTest
enable_testing()
# # add_subdirectory作用是什么？？
# The add_subdirectory(test/ctest) command is used in CMake to add a subdirectory to the build.
# It tells CMake to look for a CMakeLists.txt file in the specified directory and include it in the build process.

# The CMakeLists.txt file in the specified directory can contain additional instructions for building the code
# in that directory. This is useful for organizing large projects into smaller, more manageable pieces.
#
# In summary, add_subdirectory(test/ctest) adds a subdirectory to the build process and includes any additional
# build instructions specified in the CMakeLists.txt file in that directory.
add_subdirectory(test/ctest)



# --------------------------------- Questions ------------------------------------------
# Q1. what is target ?
# A: Target is an executable or a library to be built using a CMake script.


# Q2. what is executable ?
# A: An executable is a file that can be run on a computer to perform a specific task. 
#    In the context of the code you provided in home/yr/yr/code/clion_example/cmake_testapp/CMakeLists.txt, 
#    the add_executable command is used to define an executable target named cmake_testapp. 
#    This command tells CMake to compile the main.cpp source file and generate an executable binary named cmake_testapp. 
#    The add_executable command creates an executable target with the specified name and source file, 
#    which will be built when the CMake project is built.


# Q3. what difference of add_library and target_link_library ??
# The main difference between add_library and target_link_libraries is their purpose in the CMake build process:
# 1. add_library: This command is used to create a library target from the specified source files. It defines a new 
#   library target with a given name and type (e.g., STATIC, SHARED, or MODULE). The library target can then be linked 
#   to other targets using the target_link_libraries command.
# Here's the relevant code snippet from your CMakeLists.txt file:
# In this example, add_library creates a static library target named test_library from the calc.cpp source file.

# 2. target_link_libraries: This command is used to link a target (usually an executable) with one or more libraries. 
#   It specifies the libraries that should be linked to a target and their linking properties (e.g., PUBLIC, PRIVATE, or INTERFACE).
# Here's the relevant code snippet from your CMakeLists.txt file:
#   find_library(TEST_LIBRARY test_library lib)
#   target_link_libraries(cmake_testapp LINK_PUBLIC ${TEST_LIBRARY})

# In this example, find_library locates the test_library and assigns its path to the TEST_LIBRARY variable. 
# Then, target_link_libraries links the cmake_testapp executable target with the library specified in the ${TEST_LIBRARY} variable 
# using the LINK_PUBLIC option.

# In summary, add_library is used to create a library target from source files, 
# while target_link_libraries is used to link a target with one or more libraries.

# Q4. what is find_package() include_directories() and target_link_libraries() ??

# Q5. add_library()

# Q6. target_link_libraries(), what parameters of target_link_libraries ??
# A: library paths or library name ?? what paths of target_link_libraries to search ?