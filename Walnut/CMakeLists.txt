project("Walnut" LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)
message("Configuring ${PROJECT_NAME}")

file(GLOB_RECURSE WALNUT_SOURCE_FILES
	"src/Walnut/*.h"
	"src/Walnut/*.cpp"
	"src/Walnut/Input/*.cpp"
	"src/Walnut/Input/*.h"
)
message("----------")
message("Walnut source files ${WALNUT_SOURCE_FILES}")
file(GLOB IMGUI_SOURCE_FILES
		"${IMGUI_INCLUDE_DIR}/*.cpp"
		"${IMGUI_INCLUDE_DIR}/*.h"
		"${IMGUI_INCLUDE_DIR}/backends/imgui_impl_vulkan.cpp"
		"${IMGUI_INCLUDE_DIR}/backends/imgui_impl_glfw.cpp"
		)
message("----------")
message("Imgui source files ${IMGUI_SOURCE_FILES}")
message("----------")
add_library("${PROJECT_NAME}"
	"${WALNUT_SOURCE_FILES};${IMGUI_SOURCE_FILES}"
	)

target_include_directories("${PROJECT_NAME}" PUBLIC
		"${GLM_INCLUDE_DIR}"
		"${GLFW_INCLUDE_DIR}"
		"${VULKAN_INCLUDE_DIR}"
		"${IMGUI_INCLUDE_DIR}"
		"${CMAKE_SOURCE_DIR}/vendor/imgui"
		"${IMGUI_INCLUDE_DIR}/backends"
		"${STB_INCLUDE_DIR}")

target_link_libraries("${PROJECT_NAME}" PUBLIC
		"${VULKAN_LIB}" glfw)

target_compile_definitions("${PROJECT_NAME}" PRIVATE
	$<IF:$<CONFIG:Debug>,WL_DEBUG,>
	$<IF:$<CONFIG:Release>,WL_RELEASE,>
	$<IF:$<PLATFORM_ID:Windows>,WL_PLATFORM_WINDOWS,>
	$<IF:$<PLATFORM_ID:Darwin>,WL_PLATFORM_MACOS,>
)
