
cmake_minimum_required(VERSION 3.8)
PROJECT(any_container_test)
#dependency


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(MSVC)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++latest")
endif(MSVC)

# add json support
find_package(nlohmann_json CONFIG REQUIRED)


add_executable(encode_test ${CMAKE_CURRENT_SOURCE_DIR}/encode/encode_test.cpp)
target_link_libraries(encode_test PUBLIC nlohmann_json::nlohmann_json)

add_executable(decode_test ${CMAKE_CURRENT_SOURCE_DIR}/decode/decode_test.cpp)
target_link_libraries(decode_test PUBLIC nlohmann_json::nlohmann_json)


