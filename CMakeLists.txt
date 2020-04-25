cmake_minimum_required(VERSION 3.5)

project(gstbt LANGUAGES CXX C)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(PkgConfig REQUIRED)
pkg_search_module(GST REQUIRED gstreamer-1.0)
pkg_search_module(LIBTORRENT REQUIRED libtorrent-rasterbar)

include_directories(
    ${GST_INCLUDE_DIRS} ${GST_BASE_INCLUDE_DIRS} ${LIBTORRENT_INCLUDE_DIRS}
    )

link_libraries(
    ${GST_LDFLAGS} ${GST_BASE_LDFLAGS} ${LIBTORRENT_LDFLAGS}
    )

set(src_list
    "src/gst_bt_demux.cpp"
    "src/gst_bt_src.cpp"
    "src/gst_bt_type.c"
    "src/gst_bt.c"
    )

if (WIN32)
message(STATUS "target system: WIN32")
endif()

if (MSVC)
message(STATUS "useing MSVC")
endif()

add_library(${PROJECT_NAME} SHARED ${src_list})
add_library(${PROJECT_NAME}_static STATIC ${src_list})
