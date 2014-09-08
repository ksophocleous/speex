cmake_minimum_required(VERSION 2.8)

project(speex)

set(SPEEX_LIBRARY_VERSION_MAJOR 1)
set(SPEEX_LIBRARY_VERSION_MINOR 1)
set(SPEEX_LIBRARY_VERSION_MICRO 16)
set(SPEEX_VERSION "1.2rc1")

# simplify output directories on platforms with multiple configurations
foreach(OUTPUTCONFIG ${CMAKE_CONFIGURATION_TYPES})
	string(TOUPPER ${OUTPUTCONFIG} OUTPUTCONFIG)
	set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/bin)
	set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/lib)
	set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/lib)
endforeach(OUTPUTCONFIG CMAKE_CONFIGURATION_TYPES)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

add_subdirectory(libspeex)

#add_executable(speexdec src/speexdec.c)
#target_link_libraries(speexdec libspeex)

#add_executable(skeleton src/skeleton.c)
#target_link_libraries(skeleton libspeex)
