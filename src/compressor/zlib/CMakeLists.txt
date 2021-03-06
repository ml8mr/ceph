# zlib

if(HAVE_INTEL_SSE4_1 AND HAVE_BETTER_YASM_ELF64 AND (NOT APPLE))
	set(zlib_sources
	  CompressionPluginZlib.cc
	  ZlibCompressor.cc
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/crc32_gzip.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/crc32_gzip_base.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/detect_repeated_char.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/encode_df.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/encode_df_04.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/flatten_ll.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/huff_codes.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/hufftables_c.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_base.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_body_01.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_body_02.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_body_04.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_finish.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_icf_base.c
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_icf_body_01.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_icf_body_02.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_icf_body_04.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_icf_finish.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_multibinary.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_update_histogram_01.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/igzip_update_histogram_04.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/proc_heap.asm
	  ${CMAKE_SOURCE_DIR}/src/isa-l/igzip/rfc1951_lookup.asm
	)
else(HAVE_INTEL_SSE4_1 AND HAVE_BETTER_YASM_ELF64 AND (NOT APPLE))
	set(zlib_sources
	  CompressionPluginZlib.cc
	  ZlibCompressor.cc
	)
endif(HAVE_INTEL_SSE4_1 AND HAVE_BETTER_YASM_ELF64 AND (NOT APPLE))

add_library(ceph_zlib SHARED ${zlib_sources})
target_link_libraries(ceph_zlib ZLIB::ZLIB ${win32_common})
target_include_directories(ceph_zlib SYSTEM PRIVATE "${CMAKE_SOURCE_DIR}/src/isa-l/include")
set_target_properties(ceph_zlib PROPERTIES
  VERSION 2.0.0
  SOVERSION 2
  INSTALL_RPATH "")
install(TARGETS ceph_zlib DESTINATION ${compressor_plugin_dir})
