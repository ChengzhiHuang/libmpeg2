SET (CMAKE_C_FLAGS_TEST " -DPROFILE_ENABLE -DARM -fPIC -DMD5_DISABLE ")
SET(libmpeg2_top_srcdir ..)
SET (mpeg2test_src_files
	decoder/main.c
)
INCLUDE_DIRECTORIES(${libmpeg2_top_srcdir}/decoder
		${libmpeg2_top_srcdir}/common
		${libmpeg2_top_srcdir}/decoder/x86
		${libmpeg2_top_srcdir}/common/x86
)#add by main.c:53:28: fatal error: iv_datatypedef.h: 没有那个文件或目录
LINK_DIRECTORIES (
		${libmpeg2_top_srcdir}/lib
		/usr/lib/android/
)
ADD_EXECUTABLE (mpeg2decode ${mpeg2test_src_files})
TARGET_LINK_LIBRARIES (mpeg2decode log mpeg2 pthread )#android-liblog-dev是原来bp文件里的shared_libs: ["liblog"] 安装在/usr/lib/android/里面
#sudo apt-get install android-liblog-dev
ADD_DEFINITIONS (${CMAKE_C_FLAGS_TEST})
SET (EXECUTABLE_OUTPUT_PATH ${libmpeg2_top_srcdir}/bin)
