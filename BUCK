include_defs('//BUCKAROO_DEPS')

genrule(
  name = 'autogen-configure',
  out = 'out',
  srcs = glob([
    'autogen.sh',
    'configure.ac',
    'Makefile.am',
    'AUTHORS',
    'ChangeLog',
    'COPYING',
    'NEWS',
    'README',
    'm4/*',
    '*.in',
  ]),
  cmd = 'cp -r $SRCDIR $OUT && cd $OUT && chmod +x ./autogen.sh && ./autogen.sh && chmod +x ./configure && ./configure',
)

genrule(
  name = 'config.h',
  out = 'config.h',
  cmd = 'cp $(location :autogen-configure)/config.h $OUT',
)

genrule(
  name = 'snappy-stubs-public.h',
  out = 'snappy-stubs-public.h',
  cmd = 'cp $(location :autogen-configure)/snappy-stubs-public.h $OUT',
)

cxx_library(
  name = 'snappy',
  header_namespace = '',
  exported_headers = glob(['*.h']) + [
    ':snappy-stubs-public.h',
  ],
  headers = [
    'snappy-stubs-internal.h',
    'snappy-internal.h',
    'snappy-sinksource.h',
    ':config.h',
  ],
  srcs = [
    'snappy-c.cc',
    'snappy.cc',
    'snappy-stubs-internal.cc',
    'snappy-sinksource.cc',
  ],
  deps = BUCKAROO_DEPS,
  visibility = [
    'PUBLIC',
  ],
)

cxx_test(
  name = 'snappy-test',
  headers = [
    'snappy-test.h',
    'snappy-stubs-internal.h',
  ],
  srcs = [
    'snappy-test.cc',
  ],
  deps = [
    ':snappy',
  ],
)
