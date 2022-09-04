cmake_minimum_required(VERSION 3.10)

project(MyApp)

set(CMAKE_EXPORT_COMPILE_COMMANDS true)

set(CMAKE_CONFIGURATION_TYPES "Debug" "Release")

# Windows only. Needed to make sure that both the .dll and .lib files are created for any shared library
if(CMAKE_HOST_WIN32)
	set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS 1)
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/Debug/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/Debug/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/Debug/bin)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/Release/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/Release/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/Release/bin)

set(CMAKE_INSTALL_PREFIX dist/MyApp-linux-x86_64)

add_subdirectory(src)

include(InstallRequiredSystemLibraries)
set(CPACK_SOURCE_GENERATOR "TGZ")
include(CPack)
