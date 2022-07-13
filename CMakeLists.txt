cmake_minimum_required(VERSION 3.2)
project(AVIMediaPlayer)
add_definitions(-D__WIIU__ -D__wiiu__ -D__WUT__ -D__wut__)

add_executable(mediap
                src/main.c
                src/screen.c
                src/app.c
                src/monitor.c
                src/decoder/avi-mjpeg.c)
target_include_directories(mediap PRIVATE ${DEVKITPRO}/portlibs/ppc/include)
target_link_directories(mediap PRIVATE ${DEVKITPRO}/portlibs/ppc/lib)
target_link_libraries(mediap
    wut
    turbojpeg)

include_directories(${CMAKE_SOURCE_DIR}/ext/include)

include_directories(${CMAKE_SOURCE_DIR}/src)
set_property(TARGET mediap PROPERTY C_STANDARD 99)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra")
wut_create_rpx(mediap)