cmake_minimum_required(VERSION 3.0)

project(quickjs)

add_library(quickjs STATIC
	"${CMAKE_CURRENT_SOURCE_DIR}/quickjs.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/libbf.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/libregexp.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/libunicode.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/cutils.c"
)
target_include_directories(quickjs PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(quickjs PROPERTIES C_STANDARD 11)

file(READ "${CMAKE_CURRENT_SOURCE_DIR}/VERSION" quickjs_VERSION_DATA)
string(STRIP "${quickjs_VERSION_DATA}" quickjs_VERSION)

target_compile_definitions(quickjs PRIVATE
	"CONFIG_VERSION=\"${quickjs_VERSION}\""
	"CONFIG_BIGNUM"
	"EMSCRIPTEN"
)
