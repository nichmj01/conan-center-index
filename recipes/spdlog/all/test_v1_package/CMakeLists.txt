cmake_minimum_required(VERSION 3.8)
project(test_package LANGUAGES CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(TARGETS)

find_package(spdlog REQUIRED CONFIG)

add_executable(${PROJECT_NAME} ../test_package/test_package.cpp)
if(TARGET spdlog::spdlog_header_only)
    target_link_libraries(${PROJECT_NAME} spdlog::spdlog_header_only)
else()
    target_link_libraries(${PROJECT_NAME} spdlog::spdlog)
endif()
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_11)
