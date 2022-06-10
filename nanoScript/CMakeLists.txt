# CMakeList.txt : CMake project for nanoScript, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(EXECUTABLE_SRC "src/nanoScriptMain.cpp;src/nanoScriptMain.h")
set(LIBRARY_SRC "src/nanoScript.cpp;src/nanoScript.h")

# Check what to compile the project to. If it's compiled as a standalone
# it will be compiled as a commandline tool/REPl. If it's included as a
# library it will be compiled only as a library

if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
	
	message(STATUS "Building nanoScript as executable!")
	
	add_executable (nanoScript 
		${EXECUTABLE_SRC}
		${LIBRARY_SRC}
	)
else()
	
	message(STATUS "Building nanoScript as library!")

	add_library (nanoScript
		${LIBRARY_SRC}
	)

	target_include_directories(nanoScript
		PRIVATE
			${CMAKE_CURRENT_SOURCE_DIR}/src
		PUBLIC
			$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
	)
endif()

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET nanoScript PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
