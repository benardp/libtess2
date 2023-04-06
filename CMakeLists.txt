cmake_minimum_required(VERSION 3.14)
project(libtess2)

set(LIBTESS2_INCLUDE
	Include/tesselator.h
)

set(LIBTESS2_SOURCE
	Source/bucketalloc.c
	Source/dict.c
	Source/geom.c
	Source/mesh.c
	Source/priorityq.c
	Source/sweep.c
	Source/tess.c
	Source/bucketalloc.h
	Source/dict.h
	Source/geom.h
	Source/mesh.h
	Source/priorityq.h
	Source/sweep.h
	Source/tess.h
)

if (WIN32) {
	add_library(libtess2 STATIC ${LIBTESS2_SOURCE} ${LIBTESS2_INCLUDE})
} else {
	add_library(libtess2 ${LIBTESS2_SOURCE} ${LIBTESS2_INCLUDE})
}

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/Include)

file(WRITE "${CMAKE_BINARY_DIR}/libtess2-config.cmake" "include(\"\${CMAKE_CURRENT_LIST_DIR}/libtess2-targets.cmake\")")
install(FILES "${CMAKE_BINARY_DIR}/libtess2-config.cmake" DESTINATION "share/libtess2/")

install(TARGETS libtess2 EXPORT libtess2-targets)

install(EXPORT libtess2-targets DESTINATION share/libtess2/)

install(FILES ${LIBTESS2_INCLUDES} DESTINATION include/libtess2)