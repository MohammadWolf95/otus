cmake_minimum_required(VERSION 3.2)

project(Allocate VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})

# set variables for directories with source code
set(SOURCE_PATH "${PROJECT_SOURCE_DIR}/src")
#set(TEST_PATH "${PROJECT_SOURCE_DIR}/tests")

find_package(Boost COMPONENTS unit_test_framework REQUIRED)

#configure_file(${SOURCE_PATH}/version.h.in version.h)

add_executable(allocate ${SOURCE_PATH}/main.cpp)

add_library(NewDelete ${SOURCE_PATH}/newdelete.cpp)

#add_executable(test_main_exe test_main.cpp)

set_target_properties(allocate PROPERTIES
	CXX_STANDARD 14
	CXX_STANDARD_REQUIRED ON
	COMPILE_OPTIONS -Wpedantic -Wall -Wextra -std=c++14
)

#set_target_properties(test_main_exe PROPERTIES
#  COMPILE_DEFINITIONS BOOST_TEST_DYN_LINK
#  INCLUDE_DIRECTORIES ${Boost_INCLUDE_DIR}
#)

target_link_libraries(allocate NewDelete)

#target_link_libraries(test_main_exe
#  ${Boost_LIBRARIES}
#  HelloWorld
#)

install(TARGETS allocate RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT abdulvadudovmagomed@mail.ru)

include(CPack)

#enable_testing()

#add_test(test_version_valid test_main_exe)
