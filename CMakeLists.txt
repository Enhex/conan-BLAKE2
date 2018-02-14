cmake_minimum_required(VERSION 3.8)

include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake)


project(BLAKE2)
conan_basic_setup()

include_directories(include)

if(${SSE})
	file(GLOB_RECURSE SourceFiles
		"BLAKE2/sse/blake2*.h"
		"BLAKE2/sse/blake2*.c"
	)
else()
	file(GLOB_RECURSE SourceFiles
		"BLAKE2/ref/blake2*.h"
		"BLAKE2/ref/blake2*.c"
	)
endif()

set(TargetName BLAKE2)
add_library(${TargetName} ${SourceFiles})
conan_target_link_libraries(${TargetName})

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${TargetName})