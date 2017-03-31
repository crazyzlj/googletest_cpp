cmake_minimum_required(VERSION 2.8.2)

set(PROJECT_NAME_STR unittest_demo)
project(${PROJECT_NAME_STR} C CXX)
set(CMAKE_MODULE_PATH
    ${CMAKE_CURRENT_SOURCE_DIR}/cmake
    ${CMAKE_MODULE_PATH}
)
MESSAGE(${CMAKE_MODULE_PATH})
include(SetThreadFlagMSVC)
###########################################################
#########  Git clone the latest googletest   ##############
###########################################################
if (CMAKE_VERSION VERSION_LESS 3.2)
    set(UPDATE_DISCONNECTED_IF_AVAILABLE "")
else()
    set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")
endif()
include(DownloadProject)
download_project(PROJ                googletest
                 GIT_REPOSITORY      https://github.com/google/googletest.git
                 GIT_TAG             master
                 ${UPDATE_DISCONNECTED_IF_AVAILABLE}
)

# Prevent GoogleTest from overriding our compiler/linker options
# when building with Visual Studio
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})
include_directories("${gtest_SOURCE_DIR}/include" "${gmock_SOURCE_DIR}/include")

###########################################################
######                 Demo library            ############
###########################################################
set(PROJECT_LIB_NAME ${PROJECT_NAME_STR}lib)
include_directories(${PROJECT_SOURCE_DIR}/src)
file(GLOB LIB_SRC_FILES ${PROJECT_SOURCE_DIR}/src/demo.cpp)
add_library(${PROJECT_LIB_NAME} ${LIB_SRC_FILES})

###########################################################
######              unittest executable        ############
###########################################################
enable_testing()
set(PROJECT_TEST_NAME ${PROJECT_NAME_STR}_test)
file(GLOB TEST_SRC_FILES ${PROJECT_SOURCE_DIR}/test/*.cpp)
add_executable(${PROJECT_TEST_NAME} ${TEST_SRC_FILES})
target_link_libraries(${PROJECT_TEST_NAME} ${PROJECT_LIB_NAME} gtest gmock_main)
add_test(${PROJECT_TEST_NAME} ${PROJECT_TEST_NAME})

###########################################################
######                Main executable          ############
###########################################################
set(PROJECT_NAME ${PROJECT_NAME_STR})
file(GLOB MAIN_SRC_FILES ${PROJECT_SOURCE_DIR}/src/main.cpp)
add_executable(${PROJECT_NAME} ${MAIN_SRC_FILES})
target_link_libraries(${PROJECT_NAME} ${PROJECT_LIB_NAME})
