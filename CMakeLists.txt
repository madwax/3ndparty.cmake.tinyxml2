cmake_minimum_required( VERSION 3.1.0 )

project( tinyxml2 C CXX )

SET( CMAKE_INSTALL_PREFIX "" CACHE PATH "Don't want an install target" FORCE)

# We do things my submodules.
set( tinyxml2_TRUE_SOURCE_DIR "${tinyxml2_SOURCE_DIR}/tinyxml2" )

set( tinyxml2_INCLUDE_DIR ${tinyxml2_TRUE_SOURCE_DIR}/ )
set( tinyxml2_SOURCES "${tinyxml2_TRUE_SOURCE_DIR}/tinyxml2.cpp" )

set( tinyxml2_LINK "" )
set( tinyxml2_DEFINES "" )

set( tinyxml2_INCLUDE_DIR_PRIVATE "" )
set( tinyxml2_LINK_PRIVATE "" )
set( tinyxml2_DEFINES_PRIVATE "" )

if( MSVC )
	list( APPEND tinyxml2_DEFINES_PRIVATE "-D_CRT_SECURE_NO_WARNINGS" )
endif()

add_library( tinyxml2 STATIC ${tinyxml2_SOURCES} )

target_include_directories( tinyxml2 PRIVATE ${tinyxml2_INCLUDE_DIR} ${tinyxml2_INCLUDE_DIR_PRIVATE} )
target_compile_definitions( tinyxml2 PRIVATE ${tinyxml2_DEFINES} ${tinyxml2_DEFINES_PRIVATE} )
target_link_libraries( tinyxml2 PRIVATE ${tinyxml2_LINK} ${tinyxml2_LINK_PRIVATE} )

target_include_directories( tinyxml2 INTERFACE $<BUILD_INTERFACE:${tinyxml2_INCLUDE_DIR}> )
target_compile_definitions( tinyxml2 INTERFACE ${tinyxml2_DEFINES} )
target_link_libraries( tinyxml2 INTERFACE ${tinyxml2_LINK} )

