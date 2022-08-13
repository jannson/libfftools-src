cmake_minimum_required (VERSION 2.6)
project (libfftools)
set(CMAKE_VERBOSE_MAKEFILE ON)
#-m32 
#add_definitions( -O0 -g -rdynamic -fno-inline -Wstrict-prototypes -std=gnu99 -Wall)
add_definitions( -Os -Wstrict-prototypes -D_ISOC99_SOURCE -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -U__STRICT_ANSI__ -D__USE_MINGW_ANSI_STDIO=1 -D__printf__=__gnu_printf__ -D_WIN32_WINNT=0x0600 -D_POSIX_C_SOURCE=200112 -D_XOPEN_SOURCE=600 -DPIC -DZLIB_CONST -std=c11 -fomit-frame-pointer   -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/harfbuzz -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/cairo -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/pixman-1 -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/libpng16 -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/glib-2.0 -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/lib/glib-2.0/include -mms-bitfields -DPCRE_STATIC -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/fribidi -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/freetype2  -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/bs2b  -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/opus -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/opus          -Wdeclaration-after-statement -Wall -Wdisabled-optimization -Wpointer-arith -Wredundant-decls -Wwrite-strings -Wtype-limits -Wundef -Wmissing-prototypes -Wno-pointer-to-int-cast -Wstrict-prototypes -Wempty-body -Wno-parentheses -Wno-switch -Wno-format-zero-length -Wno-pointer-sign -Wno-char-subscripts -O3 -fno-math-errno -fno-signed-zeros -fno-tree-vectorize -Werror=format-security -Werror=implicit-function-declaration -Werror=missing-prototypes -Werror=return-type -Werror=vla -Wformat -fdiagnostics-color=auto -Wno-maybe-uninitialized -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/SDL2   -I/projects/github/mpv-build2/mxe/usr/x86_64-w64-mingw32.static/include/SDL2 -Dmain=SDL_main )

# CC=x86_64-w64-mingw32.static-gcc cmake -DCMAKE_SYSTEM_NAME="Windows" ..

set(CMAKE_SYSTEM_NAME Windows)
set(CMAKE_BUILD_TYPE release)
set(CMAKE_C_COMPILER_WORKS 1)
SET(CMAKE_CROSSCOMPILING 1)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)
set(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "")
set(CMAKE_SHARED_LIBRARY_LINK_CXX_FLAGS "")

set(CMAKE_C_CREATE_STATIC_LIBRARY
  "<CMAKE_AR> cr <TARGET> <LINK_FLAGS> <OBJECTS>"
  "<CMAKE_RANLIB> <TARGET>"
  )

set(FFMPEG_PATH "/projects/github/mpv-build2/ffmpeg-4.2.3")
set(MXE_PATH "/projects/github/mpv-build2/mxe")

include_directories(${FFMPEG_PATH}/build)
include_directories(${FFMPEG_PATH})
include_directories(${MXE_PATH}/usr/x86_64-w64-mingw32.static/include)

set(FFTOOLS_FILES libfftools/cmdutils.c libfftools/ffmpeg.c libfftools/ffmpeg_filter.c libfftools/ffmpeg_hw.c)

add_library(fftools ${FFTOOLS_FILES})
set_target_properties(fftools PROPERTIES LINKER_LANGUAGE C)

