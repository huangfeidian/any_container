
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
add_subdirectory(test)

add_library(${CMAKE_PROJECT_NAME} INTERFACE)
target_include_directories(${CMAKE_PROJECT_NAME} INTERFACE $<INSTALL_INTERFACE:include>)
target_link_libraries(${CMAKE_PROJECT_NAME} INTERFACE  nlohmann_json::nlohmann_json)

foreach(p LIB INCLUDE)
	set(var CMAKE_INSTALL_${p}DIR)
	if(NOT IS_ABSOLUTE "${${var}}")
                string(TOLOWER ${p} lower_p)
		set(${var} "${CMAKE_INSTALL_PREFIX}/${lower_p}")
	endif()
endforeach()

export(TARGETS ${CMAKE_PROJECT_NAME}
     FILE ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}Targets.cmake)

file(WRITE
    ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}Config.cmake
    "include(\${CMAKE_CURRENT_LIST_DIR}/${CMAKE_PROJECT_NAME}Targets.cmake)\n")

install(FILES
        ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}Config.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${CMAKE_PROJECT_NAME})

install(TARGETS ${PROJECT_NAME} EXPORT ${PROJECT_NAME}Targets
   ARCHIVE  DESTINATION lib
   LIBRARY DESTINATION lib
  )

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/ DESTINATION include/${PROJECT_NAME})

install(EXPORT ${CMAKE_PROJECT_NAME}Targets
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${CMAKE_PROJECT_NAME})
