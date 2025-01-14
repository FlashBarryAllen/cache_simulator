# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# Set the project name
project(driver)

# Set the C++ standard to C++20
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set compiler flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -march=native -mtune=native -flto -fuse-linker-plugin")

# Find the Protobuf package
find_package(Protobuf REQUIRED)

# Generate protobuf sources from cache_config.proto
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS cache_config.proto)

# List all source files
set(SOURCE_FILES
    driver.cpp
    simulation.cpp
    data_cache.cpp
    cache_set.cpp
    access.cpp
    ${PROTO_SRCS}
)

# Add the executable
add_executable(driver ${SOURCE_FILES})

# Link the Protobuf library
target_link_libraries(driver ${Protobuf_LIBRARIES})