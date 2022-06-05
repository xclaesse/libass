src_x86 = files(
    'x86/be_blur.asm',
    'x86/blend_bitmaps.asm',
    'x86/blur.asm',
    'x86/cpuid.asm',
    'x86/rasterizer.asm',
)
src_fontconfig = files('ass_fontconfig.c')
src_directwrite = files('ass_directwrite.c')
src_coretext = files('ass_coretext.c')

libass_src = files(
    'ass.c',
    'ass_bitmap.c',
    'ass_blur.c',
    'ass_cache.c',
    'ass_drawing.c',
    'ass_filesystem.c',
    'ass_font.c',
    'ass_fontselect.c',
    'ass_library.c',
    'ass_outline.c',
    'ass_parse.c',
    'ass_rasterizer.c',
    'ass_rasterizer_c.c',
    'ass_render.c',
    'ass_render_api.c',
    'ass_shaper.c',
    'ass_string.c',
    'ass_strtod.c',
    'ass_utils.c',
)

libass_headers = files(
    'ass.h',
    'ass_types.h'
)

if fontconfig
    libass_src += src_fontconfig
endif
if directwrite
    libass_src += src_directwrite
endif
if coretext
    libass_src += src_coretext
endif

if enable_asm
    libass_src += nasm_gen.process(src_x86)
endif

gen_defs = find_program('../gen_defs.py')
libass_def = custom_target('libass.def',
                           input: ['libass.sym'],
                           output: ['libass.def'],
                           command: [gen_defs, '@INPUT@', '@OUTPUT@'])

libass = library('ass', libass_src, config_h,
                 vs_module_defs: libass_def,
                 install: true,
                 include_directories: incs,
                 dependencies: deps)

libass_dep = declare_dependency(link_with: libass,
                                include_directories: incs,
                                dependencies: deps,
                                sources: config_h)

install_headers(libass_headers, subdir: 'ass')
subdir('ass')
