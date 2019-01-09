load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'cmake',
  out = 'out',
  srcs = glob([
    '*.txt',
    'cmake/**/*.cmake',
    'cmake/**/*.in',
  ]),
  cmd = 'mkdir -p $OUT && cd $OUT && cmake $SRCDIR || true',
)

genrule(
  name = 'config-h',
  out = 'turf_config.h',
  cmd = 'cp $(location :cmake)/include/turf_config.h $OUT',
)

genrule(
  name = 'userconfig-h',
  out = 'turf_userconfig.h',
  cmd = 'cp $(location :cmake)/include/turf_userconfig.h $OUT',
)

cxx_library(
  name = 'turf',
  header_namespace = '',
  exported_headers = dict(
    subdir_glob([
      ('', 'turf/**/*.h'),
      ('turf/impl', '**/*.inc'),
    ]).items() + [
      ('turf_config.h', ':config-h'),
      ('turf_userconfig.h', ':userconfig-h'),
    ]
  ),
  srcs = glob([
    'turf/**/*.cpp',
    'turf/**/*.c',
  ]),
  licenses = [
    'LICENSE',
  ],
  visibility = [
    'PUBLIC'
  ],
)
