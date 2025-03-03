cmake_minimum_required(VERSION 3.24)
project(hello)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Find SDL3
find_package(SDL3 REQUIRED)

# Add executable
add_executable(${PROJECT_NAME} src/main.cpp)

# Link SDL3
target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3)

# Copy SDL3 libraries to the build directory (if needed)
if(APPLE)
    add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        $<TARGET_FILE_DIR:SDL3::SDL3>
        $<TARGET_FILE_DIR:${PROJECT_NAME}>)
endif()
