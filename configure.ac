dnl Hey Emacs, I want this in -*- sh -*- mode, please.

dnl Copyright 1988-92, 1994-95, 1999, 2000 Free Software Foundation, Inc.
dnl Please see COPYING for a description your rights and responsibilities
dnl with this software.
dnl Process this file with autoconf to produce a configure script.

dnl ----------------------------- HOST SYSTEM --------------------------------

AC_PREREQ(2.58)
AC_REVISION($Revision: 2.5a$)
VERSION=2.5a

AC_INIT
AC_CONFIG_SRCDIR([superopt.c])
AC_PROG_CC
AC_PROG_CPP
AC_PROG_LN_S
AC_PROG_INSTALL
AC_PROG_MAKE_SET

dnl Checks for header files.
AC_HEADER_STDC
AC_HEADER_TIME
AC_CHECK_HEADERS(sys/resource.h)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_INLINE

dnl ---------------------------- COMMAND LINE ---------------------------------

AC_ARG_ENABLE(expensive-goals,
[  --enable-expensive-goals     enable 4-ary goals in make run],
, enable_expensive_goals=no)

AC_ARG_ENABLE(divmul,
[  --enable-divmul[=mul]        enable division and multiplication],
, enable_divmul=no)

AC_ARG_ENABLE(debug,
[  --enable-debug               enable debug code],
, enable_debug=no)

AC_ARG_ENABLE(stats,
[  --enable-stats               gather statistics],
, enable_stats=no)

AC_ARG_ENABLE(single,
[  --enable-single              output a single sequence satisfying the goal],
, enable_single=no)

AC_ARG_ENABLE(timing,
[  --enable-timing              measure timings],
, enable_timing=no)

if test "$enable_expensive_goals" = yes; then
  AC_DEFINE(EXPENSIVE, 1)
fi
if test "$enable_divmul" = yes; then
  AC_DEFINE(DM, 1)
fi
if test "$enable_divmul" != no; then
  AC_DEFINE(MM, 1)
fi
if test "$enable_stats" = yes; then
  AC_DEFINE(STATISTICS, 1)
fi
if test "$enable_single" = yes; then
  AC_DEFINE(SINGLE, 1)
fi
if test "$enable_timing" = yes; then
  AC_DEFINE(TIMING, 1)
fi

AC_ARG_WITH(arch,
[  --with_arch=arch1,arch2,...  choose architectures to compile], 
  [H="#"], [
  H=

  # Least general before (e.g. POWERPC before POWER)
  all_hosts="SPARC MC68020 MC68000 M88000 POWERPC POWER AM29K I386"
  all_hosts="$all_hosts I960B I960 PYR ALPHA HPPA SH"

  test "$with_arch" = "yes" && with_arch=
  test -z "$with_arch" && with_arch="$all_hosts"

  changequote(,)
  with_arch="`echo "$with_arch" | tr ",[A-Z]" " [a-z]"`"

  changequote([,])
  HOST_ARCH=
  for i in $all_hosts; do
    AC_EGREP_CPP(got-the-host, [
      #include "superopt.h"
      #if $i
      got-the-host
      #endif
    ], [
      HOST_ARCH=`echo $i | tr "[A-Z]" "[a-z]"`
      break
    ])
  done
  if test -z "$HOST_ARCH"; then
    AC_MSG_ERROR(Host instruction set not supported, use --with-arch)
  fi
  with_arch=$HOST_ARCH
])

ALL_MACHINES="`for i in $with_arch; do echo superopt-$i; done`"
ALL_RESULTS="`for i in $with_arch; do echo $i.res; done`"

dnl --------------------------- PRODUCE OUTPUT --------------------------------

AC_SUBST(HOST_ARCH)
AC_SUBST(ALL_MACHINES)
AC_SUBST(ALL_RESULTS)
AC_SUBST(VERSION)
AC_SUBST(H)
AC_CONFIG_FILES([Makefile version-stamp:version.h.in])
AC_CONFIG_COMMANDS([version.h],[[
  test ! -f version.h && mv version-stamp version.h
  if test -f version-stamp; then
    cmp -s version-stamp version.h || mv version-stamp version.h
  fi
  if test -f version-stamp; then
    # Still surviving...
    rm -f version-stamp
  else
    echo creating version.h
  fi
]])
AC_OUTPUT
