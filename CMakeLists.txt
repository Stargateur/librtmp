cmake_minimum_required(VERSION 3.7)
project(librtmp)
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
if(WIN32)
  target_link_libraries(rtmp PUBLIC ws2_32)
endif()
target_compile_definitions(rtmp PUBLIC -DNO_CRYPTO)
