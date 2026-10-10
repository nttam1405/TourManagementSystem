cmake_minimum_required(VERSION 3.16)
project(TourManagementSystem LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(MSVC)
  add_compile_options(/W4)
else()
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Toàn bộ .cpp trừ main.cpp gom thành thư viện lõi để chương trình chính và test dùng chung
file(GLOB_RECURSE TMS_SOURCES CONFIGURE_DEPENDS ${CMAKE_SOURCE_DIR}/src/*.cpp)
list(FILTER TMS_SOURCES EXCLUDE REGEX ".*/src/main\\.cpp$")

add_library(tms_core STATIC ${TMS_SOURCES})
target_include_directories(tms_core PUBLIC ${CMAKE_SOURCE_DIR}/include)

add_executable(tms src/main.cpp)
target_link_libraries(tms PRIVATE tms_core)

# Test: bật bằng  cmake -DBUILD_TESTS=ON ..   (mỗi file tests/test_*.cpp là một chương trình, cần có main())
option(BUILD_TESTS "Build unit tests" OFF)
if(BUILD_TESTS)
  enable_testing()
  file(GLOB TEST_SOURCES CONFIGURE_DEPENDS ${CMAKE_SOURCE_DIR}/tests/test_*.cpp)
  foreach(test_src ${TEST_SOURCES})
    get_filename_component(test_name ${test_src} NAME_WE)
    add_executable(${test_name} ${test_src})
    target_link_libraries(${test_name} PRIVATE tms_core)
    add_test(NAME ${test_name} COMMAND ${test_name})
  endforeach()
endif()
