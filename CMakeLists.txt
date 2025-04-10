cmake_minimum_required(VERSION 3.15)
project(P2P-Chat)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set the path to the global vcpkg installation using the VCPKG_ROOT environment variable
# This ensures we use the globally installed packages
if(DEFINED ENV{VCPKG_ROOT})
    set(VCPKG_PATH $ENV{VCPKG_ROOT})
else()
    message(FATAL_ERROR "Please set the VCPKG_ROOT environment variable to your global vcpkg installation.")
endif()

# Use the global vcpkg toolchain file
set(CMAKE_TOOLCHAIN_FILE "${VCPKG_PATH}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "vcpkg toolchain file")

# Závislosti (Dependencies)
find_package(Boost REQUIRED COMPONENTS beast)
find_package(nlohmann_json CONFIG REQUIRED)

# Manually add the path to termcolor (header-only) if it's installed with vcpkg
# This ensures you use termcolor from the global vcpkg installation
include_directories("${VCPKG_PATH}/installed/x64-windows/include")

# Create the executable
add_executable(p2p_chat src/main.cpp)

# Link the necessary libraries
target_link_libraries(p2p_chat PRIVATE
    Boost::beast
    nlohmann_json::nlohmann_json
)
