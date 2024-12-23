cmake_minimum_required(VERSION 3.18 FATAL_ERROR)
project(Farming)

set(CWD ${CMAKE_CURRENT_LIST_DIR})
set(CMAKE_EXPORT_COMPILE_COMMANDS True)

# APPLICATION
file(GLOB_RECURSE GAME_SOURCES 
	"src/*.cpp"
	"src/*.hpp"
)

set(EXEC_VARIABLE)
if (WIN32)
	set(EXEC_VARIABLE WIN32)
endif(WIN32)
add_executable(${PROJECT_NAME} ${EXEC_VARIABLE} ${GAME_SOURCES})

set_target_properties(${PROJECT_NAME} PROPERTIES
	CXX_STANDARD 20
	CXX_STANDARD_REQUIRED ON
)
target_include_directories(${PROJECT_NAME} PUBLIC ${CWD}/src)

add_subdirectory(libs)

target_link_libraries(Farming PUBLIC
	fmt
	jsoncpp_static
)

set_target_properties(${PROJECT_NAME} PROPERTIES
	RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}
	RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_SOURCE_DIR}
	RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_SOURCE_DIR}
)

if (WIN32)
	target_compile_definitions(${PROJECT_NAME} PRIVATE WIN32)
endif(WIN32)
