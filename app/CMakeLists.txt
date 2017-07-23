cmake_minimum_required(VERSION 3.4.1)

#使用polarssl编译
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DUSE_POLARSSL -Wmissing-declarations -Wmissing-prototypes")
include_directories(src/main/cpp/polarssl)
include_directories(src/main/cpp)
include_directories(src/main/cpp/zlib)
add_library(
             rtmp
             SHARED
             src/main/cpp/amf.c
              src/main/cpp/hashswf.c
              src/main/cpp/log.c
              src/main/cpp/parseurl.c
              src/main/cpp/rtmp.c)

add_library(polarssl SHARED IMPORTED)
add_library(z SHARED IMPORTED)
set_target_properties(polarssl PROPERTIES IMPORTED_LOCATION
                      ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libpolarssl.so)
set_target_properties(z PROPERTIES IMPORTED_LOCATION
                    ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libz.so)
target_link_libraries(
                       rtmp
                       ${log-lib}
                       polarssl
                       z)