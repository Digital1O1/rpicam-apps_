cmake_minimum_required(VERSION 3.6)

project(SimpleCam
    DESCRIPTION "A small and documented example application for libcamera"
    LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS "-Wall -Winvalid-pch -Wnon-virtual-dtor -Wextra -Werror -Wno-unused-parameter")

find_package(PkgConfig)
find_package(OpenCV REQUIRED)
find_package(Boost REQUIRED COMPONENTS program_options) # Add this line

pkg_check_modules(LIBCAMERA REQUIRED IMPORTED_TARGET libcamera)
message(STATUS "libcamera library found:")
message(STATUS "    version: ${LIBCAMERA_VERSION}")
message(STATUS "    libraries: ${LIBCAMERA_LINK_LIBRARIES}")
message(STATUS "    include path: ${LIBCAMERA_INCLUDE_DIRS}")

pkg_check_modules(LIBEVENT REQUIRED IMPORTED_TARGET libevent_pthreads)
message(STATUS "libevent_pthreads library found:")
message(STATUS "    version: ${LIBEVENT_VERSION}")
message(STATUS "    libraries: ${LIBEVENT_LINK_LIBRARIES}")
message(STATUS "    include path: ${LIBEVENT_INCLUDE_DIRS}")

include_directories(${CMAKE_SOURCE_DIR} ${LIBCAMERA_INCLUDE_DIRS} ${LIBEVENT_INCLUDE_DIRS})
include_directories("/home/pi/libcamera/include")
include_directories("/home/pi/rpicam-apps")
include_directories(${Boost_INCLUDE_DIRS}) # Add this line

set(RPICAM_APPS_CORE_DIR "/home/pi/rpicam-apps/core")

add_executable(simple-cam 
    rpicam_hello.cpp 
    ${RPICAM_APPS_CORE_DIR}/options.cpp 
    ${RPICAM_APPS_CORE_DIR}/rpicam_app.cpp
	/home/pi/rpicam-apps/build/core/version.cpp
	/home/pi/rpicam-apps/core/dma_heaps.cpp
	/home/pi/rpicam-apps/core/post_processor.cpp
	/home/pi/rpicam-apps/preview/preview.cpp
	/home/pi/rpicam-apps/core/buffer_sync.cpp
	/home/pi/rpicam-apps/core/post_processor.cpp
	/home/pi/rpicam-apps/preview/preview.cpp
	/home/pi/rpicam-apps/preview/null_preview.cpp
	/home/pi/rpicam-apps/post_processing_stages/post_processing_stage.cpp
)

target_link_libraries(simple-cam ${OpenCV_LIBS})
target_link_libraries(simple-cam PkgConfig::LIBEVENT)
target_link_libraries(simple-cam PkgConfig::LIBCAMERA)
target_link_libraries(simple-cam ${Boost_LIBRARIES}) # Add this line
