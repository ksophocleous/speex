
option(BUILD_SHARED_LIBS "Build shared version libspeex" ON)

list(APPEND srcs
	"bits.c"
	"cb_search.c"
	"exc_10_16_table.c"
	"exc_10_32_table.c"
	"exc_20_32_table.c"
	"exc_5_256_table.c"
	"exc_5_64_table.c"
	"exc_8_128_table.c"
	"fftwrap.c"
	"filters.c"
	"gain_table.c"
	"gain_table_lbr.c"
	"hexc_10_32_table.c"
	"hexc_table.c"
	"high_lsp_tables.c"
	"kiss_fft.c"
	"kiss_fftr.c"
	"lpc.c"
	"lsp.c"
	"lsp_tables_nb.c"
	"ltp.c"
	"modes.c"
	"modes_wb.c"
	"nb_celp.c"
	"quant_lsp.c"
	"sb_celp.c"
	"smallft.c"
	"speex.c"
	"speex_callbacks.c"
	"speex_header.c"
	"stereo.c"
	# "testenc.c"
	# "testenc_uwb.c"
	# "testenc_wb.c"
	"vbr.c"
	"vorbis_psy.c"
	"vq.c"
	"window.c"
	)

list(APPEND hdrs
	"_kiss_fft_guts.h"
	"arch.h"
	"bfin.h"
	"cb_search.c"
	"cb_search.h"
	"cb_search_arm4.h"
	"cb_search_bfin.h"
	"cb_search_sse.h"
	"fftwrap.h"
	"filters.h"
	"filters_arm4.h"
	"filters_bfin.h"
	"filters_sse.h"
	"fixed_arm4.h"
	"fixed_arm5e.h"
	"fixed_bfin.h"
	"fixed_debug.h"
	"fixed_generic.h"
	"hexc_10_32_table.c"
	"hexc_table.c"
	"high_lsp_tables.c"
	"kiss_fft.h"
	"kiss_fftr.h"
	"lpc.h"
	"lpc_bfin.h"
	"lsp.h"
	"lsp_bfin.h"
	"ltp.h"
	"ltp_arm4.h"
	"ltp_bfin.h"
	"ltp_sse.h"
	"math_approx.h"
	"misc_bfin.h"
	"modes.h"
	"nb_celp.h"
	"os_support.h"
	"quant_lsp.h"
	"quant_lsp_bfin.h"
	"sb_celp.h"
	"smallft.h"
	"speex_header.c"
	"stack_alloc.h"
	"vbr.h"
	"vorbis_psy.h"
	"vq.h"
	"vq_arm4.h"
	"vq_bfin.h"
	"vq_sse.h"
	)

list(APPEND public_hdrs
	"../include/speex/speex.h"
	"../include/speex/speex_bits.h"
	"../include/speex/speex_callbacks.h"
	"../include/speex/speex_header.h"
	"../include/speex/speex_stereo.h"
	"../include/speex/speex_types.h"
	)

list(APPEND public_include_dirs
	"${CMAKE_CURRENT_SOURCE_DIR}/../include")

list(APPEND inc_dirs
	"${CMAKE_CURRENT_SOURCE_DIR}"
	"${CMAKE_CURRENT_SOURCE_DIR}/../win32"
	"${public_include_dirs}")

list(APPEND definitions
	"HAVE_CONFIG_H"
	"_CRT_SECURE_NO_WARNINGS"
	"LIBSPEEX_EXPORT")

if(BUILD_SHARED_LIBS)
	set(LIBTYPE SHARED)
	list(APPEND definitions "LIBSPEEX_DLL_EXPORT")
	list(APPEND public_definitions "LIBSPEEX_DLL_IMPORT")
else()
	set(LIBTYPE STATIC)
endif()

add_library(libspeex ${LIBTYPE} ${srcs} ${hdrs} ${public_hdrs})
set_target_properties(libspeex PROPERTIES
	PUBLIC_HEADERS "${public_hdrs}"
	INCLUDE_DIRECTORIES "${inc_dirs}"
	COMPILE_DEFINITIONS "${definitions}"
	INTERFACE_INCLUDE_DIRECTORIES "${public_include_dirs}"
	INTERFACE_COMPILE_DEFINITIONS "${public_definitions}"
	PREFIX ""
	SOVERSION "${SPEEX_LIBRARY_VERSION_MAJOR}"
	)
