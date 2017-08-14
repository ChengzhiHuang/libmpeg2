PROJECT (libmpeg2)

SET(CMAKE_C_FALGS " -D_LIB -DMULTICORE -fPIC -O3 -DANDROID -Werror ")
SET(CMAKE_C_FALGS_x86 " -DX86 -DDISABLE_AVX2 -msse4.2 -mno-avx -DDEFAULT_ARCH=D_ARCH_X86_SSE42 ")

SET(libmpeg2_top_srcdir ..)
SET (mpeg2_src_files_common
		../common/impeg2_buf_mgr.c
		../common/impeg2_disp_mgr.c
		../common/impeg2_format_conv.c
        ../common/impeg2_globals.c
        ../common/impeg2_idct.c
        ../common/impeg2_inter_pred.c
        ../common/impeg2_job_queue.c
        ../common/impeg2_mem_func.c
        ../common/ithread.c
        ../decoder/impeg2d_api_main.c
        ../decoder/impeg2d_bitstream.c
        ../decoder/impeg2d_debug.c
        ../decoder/impeg2d_dec_hdr.c
        ../decoder/impeg2d_decoder.c
        ../decoder/impeg2d_d_pic.c
        ../decoder/impeg2d_function_selector_generic.c
        ../decoder/impeg2d_globals.c
        ../decoder/impeg2d_i_pic.c
        ../decoder/impeg2d_mc.c
        ../decoder/impeg2d_mv_dec.c
        ../decoder/impeg2d_pic_proc.c
        ../decoder/impeg2d_pnb_pic.c
        ../decoder/impeg2d_vld.c
        ../decoder/impeg2d_vld_tables.c
        ../decoder/impeg2d_deinterlace.c
        ../common/icv_sad.c
        ../common/icv_variance.c
        ../common/ideint.c
        ../common/ideint_cac.c
        ../common/ideint_debug.c
        ../common/ideint_function_selector_generic.c
        ../common/ideint_utils.c
)
SET (mpeg2_src_files_x86
	../decoder/x86/impeg2d_function_selector.c
	../decoder/x86/impeg2d_function_selector_avx2.c
        ../decoder/x86/impeg2d_function_selector_ssse3.c
        ../decoder/x86/impeg2d_function_selector_sse42.c
        ../common/x86/ideint_function_selector.c
        ../common/x86/ideint_function_selector_ssse3.c
        ../common/x86/ideint_function_selector_sse42.c
        ../common/x86/icv_variance_ssse3.c
        ../common/x86/icv_sad_ssse3.c
        ../common/x86/ideint_cac_ssse3.c
        ../common/x86/ideint_spatial_filter_ssse3.c
        ../common/x86/impeg2_idct_recon_sse42_intr.c
        ../common/x86/impeg2_inter_pred_sse42_intr.c
        ../common/x86/impeg2_mem_func_sse42_intr.c
)

INCLUDE_DIRECTORIES(
	${libmpeg2_top_srcdir}/decoder
	${libmpeg2_top_srcdir}/decoder/x86
	${libmpeg2_top_srcdir}/common
	${libmpeg2_top_srcdir}/common/x86
)

ADD_DEFINITIONS (${CMAKE_C_FLAGS} ${CMAKE_C_FALGS_x86})

ADD_LIBRARY (mpeg2 STATIC ${mpeg2_src_files_common} ${mpeg2_src_files_x86})

SET(LIBRARY_OUTPUT_PATH ${libmpeg2_top_srcdir}/lib)
