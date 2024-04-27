project("Walnut" LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)

file(GLOB_RECURSE WALNUT_SOURCE_FILES "src/*.h" "src/**.cpp")

file(GLOB IMGUI_SOURCE_FILES
		"${CMAKE_SOURCE_DIR}/vendor/imgui/*.cpp")

target_include_directories("${PROJECT_NAME}" INTERFACE
		"${GLM_INCLUDE_DIR}"
		"${GLFW_INCLUDE_DIR}"
		"${VULKAN_INCLUDE_DIR}"
		"${STB_INCLUDE_DIR}")

target_link_libraries("${PROJECT_NAME}" STATIC
		"${VULKAN_LIB}"
		imgui)

add_library("${PROJECT_NAME}" "${WALNUT_SOURCE_FILES}" IMGUI_SOURCE_FILES)

