
cmake_minimum_required(VERSION 3.8)
PROJECT(any_container)
#dependency


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(MSVC)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++latest")
endif(MSVC)

# add json support
find_package(nlohmann_json CONFIG REQUIRED)

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include)

set(META_TEST_DIR ${CMAKE_SOURCE_DIR}/test)


add_executable(encode_test ${META_TEST_DIR}/encode/encode_test.cpp)
target_link_libraries(encode_test PUBLIC nlohmann_json::nlohmann_json)

add_executable(decode_test ${META_TEST_DIR}/decode/decode_test.cpp)
target_link_libraries(decode_test PUBLIC nlohmann_json::nlohmann_json)

add_executable(container_test ${META_TEST_DIR}/container/container.cpp)
target_link_libraries(container_test PUBLIC nlohmann_json::nlohmann_json)

add_executable(any_value_test ${META_TEST_DIR}/any_value/any_value.cpp)
target_link_libraries(any_value_test PUBLIC nlohmann_json::nlohmann_json)
