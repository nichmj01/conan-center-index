cmake_minimum_required(VERSION 3.1.2)
project(test_package CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(TARGETS)

find_package(GTest REQUIRED)

if(WITH_MAIN)
    add_executable(${PROJECT_NAME} ../test_package/test_package.cpp)
else()
    add_executable(${PROJECT_NAME} ../test_package/main.cpp ../test_package/test_package.cpp)
endif()

if(WITH_MAIN)
    target_link_libraries(${PROJECT_NAME} GTest::gtest GTest::gtest_main)
    if(WITH_GMOCK)
        target_link_libraries(${PROJECT_NAME} GTest::gmock GTest::gmock_main)
    endif()
else()
    target_link_libraries(${PROJECT_NAME} GTest::gtest)
    if(WITH_GMOCK)
        target_link_libraries(${PROJECT_NAME} GTest::gmock)
    endif()
endif()

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
if(WITH_GMOCK)
    target_compile_definitions(${PROJECT_NAME} PRIVATE WITH_GMOCK)
endif()
