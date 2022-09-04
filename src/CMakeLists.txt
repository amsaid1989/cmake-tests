cmake_minimum_required(VERSION 3.10)

add_library(MyLib SHARED mylib.cpp)
target_include_directories(MyLib PUBLIC ../include)

add_executable(MyApp main.cpp)
target_include_directories(MyApp PUBLIC ../include)
target_link_libraries(MyApp PUBLIC MyLib)

# Linux only. Needed to point the binary to the location of the shared object
if (CMAKE_HOST_UNIX)
	set_target_properties(MyApp
		PROPERTIES
			INSTALL_RPATH "$ORIGIN/../lib"
	)
endif()

install(FILES ../include/mylib.h
	CONFIGURATIONS Release
	DESTINATION include
)
install(TARGETS MyLib MyApp
	CONFIGURATIONS Release
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
)
