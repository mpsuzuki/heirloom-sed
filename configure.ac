AC_PREREQ([2.62])
AC_INIT([heirloom-sed], [0.0.20241013], [https://github.com/mpsuzuki/heirloom-oawk/-/issues])
AM_INIT_AUTOMAKE([foreign])

# Set default prefix
AC_PREFIX_DEFAULT(["/usr/ccs"])

# Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_RANLIB

# Checks for <wchar.h> and wcwidth()
AC_CHECK_HEADER([wchar.h],[],[AC_MSG_ERROR([wchar.h is required])])
AC_CHECK_DECL([wcwidth(wchar_t)],[],[],[#include <wchar.h>])
if test x${ac_cv_have_decl_wcwidth} != xyes
then
  AC_MSG_CHECKING([-D_XOPEN_SOURCE enables the declaration of wcwidth()])
  AC_COMPILE_IFELSE([AC_LANG_SOURCE([
#define _XOPEN_SOURCE
#include <wchar.h>
],[
  (void)wcwidth;
])],[
    AC_MSG_RESULT([yes])
    CFLAGS="${CFLAGS} -D_XOPEN_SOURCE"
  ],[
    AC_MSG_ERROR([no])
  ])
fi
AC_CHECK_FUNC([wcwidth],[],[AC_MSG_ERROR([wcwidth() is required])])

# Pack included heirloom-libXXX in make dist, subdirectories must be configured always.
AC_CONFIG_SUBDIRS([heirloom-libcommon])
AC_CONFIG_SUBDIRS([heirloom-libuxre])

HEIRLOOM_FIND_LIBCOMMON
HEIRLOOM_FIND_LIBUXRE


AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([GNUmakefile])
AC_OUTPUT
