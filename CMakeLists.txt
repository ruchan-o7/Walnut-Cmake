cmake_minimum_required(VERSION 3.20)
project(WalnutApp LANGUAGES CXX C)

find_package(Vulkan REQUIRED)

set(GLM_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/vendor/glm")
set(GLFW_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/vendor/GLFW/include")
set(VULKAN_INCLUDE_DIR "${Vulkan_INCLUDE_DIR}")
set(STB_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/vendor/stb_image")
set(IMGUI_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/vendor/imgui")

set(VULKAN_LIB "${Vulkan_LIBRARIES}")

add_subdirectory(Walnut)
add_subdirectory(WalnutApp)
