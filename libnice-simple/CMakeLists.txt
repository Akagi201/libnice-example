cmake_minimum_required(VERSION 3.7.1)

project(libnice_simple)

set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

find_package(PkgConfig REQUIRED)
find_package(Intl REQUIRED)
pkg_search_module(GLIB REQUIRED glib-2.0)
pkg_search_module(NICE REQUIRED nice)

set(SRC_LIST
  libnice_simple.c
)

include_directories("/usr/local/include")

link_directories("/usr/local/lib")

add_executable(libnice_simple ${SRC_LIST})

target_include_directories(libnice_simple SYSTEM PUBLIC ${GLIB_INCLUDE_DIRS} ${NICE_INCLUDE_DIRS} ${Intl_INCLUDE_DIRS})
target_link_libraries(libnice_simple ${GLIB_LIBRARIES} ${NICE_LIBRARIES} ${Intl_LIBRARIES})
