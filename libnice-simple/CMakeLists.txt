cmake_minimum_required(VERSION 3.7.1)

project(libnice_simple)

set (CMAKE_VERBOSE_MAKEFILE 1)

set (CMAKE_BUILD_TYPE Debug)

set (CMAKE_C_FLAGS "-Wall -Werror")

set (TARGET_EXE_NAME libnice_simple)
set (SRCS
    libnice_simple.c
)

execute_process (
        COMMAND pkg-config --cflags glib-2.0
        OUTPUT_VARIABLE GLIB_CFLAGS
        OUTPUT_STRIP_TRAILING_WHITESPACE
)
message ("GLIB_CFLAGS:" ${GLIB_CFLAGS})

execute_process (
        COMMAND pkg-config --libs glib-2.0
        OUTPUT_VARIABLE GLIB_LIBS
        OUTPUT_STRIP_TRAILING_WHITESPACE
)
message ("GLIB_LIBS:" ${GLIB_LIBS})

execute_process (
        COMMAND pkg-config --cflags nice
        OUTPUT_VARIABLE GLIB_CFLAGS
        OUTPUT_STRIP_TRAILING_WHITESPACE
)
message ("NICE_CFLAGS:" ${NICE_CFLAGS})

execute_process (
        COMMAND pkg-config --libs nice
        OUTPUT_VARIABLE GLIB_LIBS
        OUTPUT_STRIP_TRAILING_WHITESPACE
)
message ("NICE_LIBS:" ${NICE_LIBS})

set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${GLIB_CFLAGS} ${NICE_CFLAGS}")
include_directories("/usr/local/include")
link_directories("/usr/local/lib")

set (LIBS
    ${GLIB_LIBS}
    ${NICE_LIBS}
)

add_executable (${TARGET_EXE_NAME} ${SRCS})
target_link_libraries (${TARGET_EXE_NAME} ${LIBS})
