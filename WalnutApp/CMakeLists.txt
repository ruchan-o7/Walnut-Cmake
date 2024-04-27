project(WalnutApp
	LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)

file(GLOB WALNUT_APP_SOURCES "src/*.h" "src/*.cpp")

add_executable("${PROJECT_NAME}" WALNUT_APP_SOURCES)
target_compile_definitions("${PROJECT_NAME}" $<
						$<CONFIG:Debug>WL_DEBUG,
						$<CONFIG:Release>WL_RELEASE>)
target_compile_definitions("${PROJECT_NAME}" $<
						$<PLATFORM_ID:Windows>WL_PLATFORM_WINDOWS,
						$<PLATFORM_ID:Darwin>WL_PLATFORM_MACOS>)
if(CMAKE_BUILD_TYPE STREQUAL "MinSizRel")
	target_compile_options("-O3")
endif
