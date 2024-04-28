project(WalnutApp
	LANGUAGES CXX)
message("Configuring ${PROJECT_NAME}")
set(CMAKE_CXX_STANDARD 17)

file(GLOB WALNUT_APP_SOURCES
	"src/*.h" "src/*.cpp"
	)

add_executable("${PROJECT_NAME}"
	"${WALNUT_APP_SOURCES}"
		"${IMGUI_INCLUDE_DIR}/backends/imgui_impl_vulkan.cpp"
		"${IMGUI_INCLUDE_DIR}/backends/imgui_impl_glfw.cpp")

target_compile_definitions("${PROJECT_NAME}" PRIVATE
	$<IF:$<CONFIG:Debug>,WL_DEBUG,>
	$<IF:$<CONFIG:Release>,WL_RELEASE,>
	$<IF:$<PLATFORM_ID:Windows>,WL_PLATFORM_WINDOWS,>
	$<IF:$<PLATFORM_ID:Darwin>,WL_PLATFORM_MACOS,>
)
target_include_directories("${PROJECT_NAME}" PUBLIC
	"${CMAKE_SOURCE_DIR}/Walnut/src"
	"${IMGUI_INCLUDE_DIR};${VULKAN_INCLUDE_DIR}"
	)
target_link_libraries("${PROJECT_NAME}" PUBLIC "Walnut")
if(CMAKE_BUILD_TYPE STREQUAL "MinSizRel")
	target_compile_options("-O3")
endif()
