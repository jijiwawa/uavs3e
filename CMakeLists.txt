cmake_minimum_required(VERSION 2.8)

project(uavs3e)

aux_source_directory(./test DIR_SRC_TEST)
set_source_files_properties(${DIR_SRC_TEST} PROPERTIES COMPILE_FLAGS "${CMAKE_C_FLAGS}  -std=c99 -O3")

add_subdirectory(./src)
include_directories("./inc")

if(${COMPILE_10BIT})
    add_definitions(-DCOMPILE_10BIT=1)
    message("-- compile 10bit")
else()
    add_definitions(-DCOMPILE_10BIT=0)
    message("-- compile 8bit")
endif()

add_executable(uavs3enc ${DIR_SRC_TEST})

target_link_libraries(uavs3enc m)
target_link_libraries(uavs3enc uavs3e)
#target_link_libraries(uavs3enc dl)

