cmake_minimum_required(VERSION 3.0)
project(librtmp)

set(OPENSSL_USE_STATIC_LIBS=true)
set(ZLIB_USE_STATIC_LIBS=true)
FIND_PACKAGE(OpenSSL)
FIND_PACKAGE(ZLIB)

add_library(rtmp
  STATIC
  rtmp.c
  log.c
  amf.c
  hashswf.c
  parseurl.c
  amf.h
  bytes.h
  dh.h
  dhgroups.h
  handshake.h
  http.h
  log.h
  rtmp_sys.h
  rtmp.h
)
if(OPENSSL_FOUND AND ZLIB_FOUND)
  target_link_libraries(rtmp PUBLIC ${OPENSSL_LIBRARIES} ${ZLIB_LIBRARIES})
  target_include_directories(rtmp PUBLIC ${OPENSSL_INCLUDE_DIR} ${ZLIB_INCLUDE_DIRS})
  target_compile_definitions(rtmp PUBLIC -DCRYPTO=OPENSSL)
  message(STATUS "CRYPTO=OPENSSL")
else()
  target_compile_definitions(rtmp PUBLIC -DNO_CRYPTO)
endif()

if(WIN32)
  target_link_libraries(rtmp PUBLIC ws2_32)
endif()
