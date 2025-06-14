project('fuseiso', ['c'],
  version : '20070708',
  license : 'GPL-2.0-or-later',
  meson_version : '>= 0.53.0',
  default_options : [
    'buildtype=debugoptimized',
    'warning_level=3'
  ]
)

# Build options
static_build = get_option('static_build')

# Compiler flags
add_project_arguments('-D_FILE_OFFSET_BITS=64', language : 'c')
add_project_arguments('-DVERSION="@0@"'.format(meson.project_version()), language : 'c')

# Dependencies
fuse_dep = dependency('fuse', required : true, static : static_build)
glib_dep = dependency('glib-2.0', required : true, static : static_build)
zlib_dep = dependency('zlib', required : true, static : static_build)

# Source files
sources = [
  'src/fuseiso.c',
  'src/isofs.c',
  'src/isofs.h'
]

# Executable
executable('fuseiso',
  sources,
  dependencies : [fuse_dep, glib_dep, zlib_dep],
  install : true
)

# Build configuration summary
summary({
  'Build type': get_option('buildtype'),
  'Static build': static_build,
  'Compiler': meson.get_compiler('c').get_id(),
  'FUSE version': fuse_dep.version(),
  'GLib version': glib_dep.version(),
  'zlib version': zlib_dep.version(),
}, section: 'Configuration')
