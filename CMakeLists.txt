# define the minimum cmake version
cmake_minimum_required(VERSION 3.20)

# define the project name with all programming languages
project(learn2code_cpp VERSION 1.0 LANGUAGES CXX)

# define programming languages standard versions
    #cpp standard version
    set(CMAKE_CXX_STANDARD 14)
    set(CMAKE_CXX_STANDARD_REQUIRED True)

    #c standard version
    set(CMAKE_C_STANDARD 11)
    set(CMAKE_C_STANDARD_REQUIRED True)

# add compile options
add_compile_options(-Wall -Wextra -pedantic)

# add Libaries
    #for simple cases just use
    add_library(x_lib src/)
    #add static libraries to pseudo name (add all libraries with same attribute)
    add_library(x_lib_static STATIC src/)
    #add dynamic libraries to pseudo name (add all libraries with same attribute)
    add_library(x_lib_dynamic SHARED src/)

# add includes to Libraries
    #for simple cases
    target_include_directories(x_lib PUBLIC include)
    #add includes to static library 
    target_include_directories(x_lib_static PUBLIC include)
    #add includes to dynamic library 
    target_include_directories(x_lib_dynamic PUBLIC include)

# add an executable and assign files (mostly only main) to it 
# always use _exec so scripts will work 
add_executable(y_exec src/main.cpp)

# add include directory to exectuable 
target_include_directories(y_exec PRIVATE include)

# link your libraries against your executable
target_link_libraries(y_exec PRIVATE x_lib x_lib_static x_lib_dynamic)

#################################################################################
#====================================OpenCV=====================================#
#comment out if not used. Either way only opencv or everything beneath          #
# "#add Libaries" must be commented out, depending on use                       # 
#################################################################################

#search for module opencv
find_package(OpenCV)

#Continue only if opencv is found
If(OpenCV_FOUND)
	
	#add executable for opencv
	add_executable(opencv_x src/x.cpp)
	
	#include and link all opencv stuff
	target_include_directories(opencv_x PUBLIC ${OpenCV_INCLUDE_DIRS})
	target_link_libraries(opencv_x ${OpenCV_LIBRARIES})
endif()

#Outpath
target_compile_definitions(opencv_x PRIVATE OUTPATH="${CMAKE_CURRENT_BINARY_DIR}")

#################################################################################
#====================================TESTING====================================#
#################################################################################

# enable testing
enable_testing()

# check gtest
find_package(GTest REQUIRED)

# include gtest cmake
include(GoogleTest)

# create a test exectuable with functions to test (to be found in test directory)
add_executable(tests test/)

# link gtest libraries
target_link_libraries(tests PRIVATE GTest::GTest GTest::Main)

# link libraries that should be tested
target_link_libraries(tests PRIVATE x_lib x_lib_static x_lib_dynamic)

# add include directory 
target_include_directories(tests PUBLIC include)

# discover and add tests to‚ test list
gtest_discover_tests(tests)