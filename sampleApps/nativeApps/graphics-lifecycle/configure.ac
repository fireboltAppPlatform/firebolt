#
# If not stated otherwise in this file or this component's Licenses.txt file the
# following copyright and licenses apply:
#
# Copyright 2016 RDK Management
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

dnl AC_PREREQ([2.65])
AC_INIT(westeros, 1.0.0, jeff_wannamaker@cable.comcast.com,westeros)
AC_CONFIG_SRCDIR([])
AC_CONFIG_HEADERS([cfg/config.h])
AC_CONFIG_MACRO_DIR([cfg])
AC_CONFIG_AUX_DIR([cfg])
AM_INIT_AUTOMAKE([foreign no-dist-gzip dist-bzip2 1.9])
LT_INIT

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AC_PROG_CXX

# Checks for header files.
AC_CHECK_HEADERS([stdlib.h string.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T
AC_HEADER_STDBOOL

ENABLE_WESTEROS_TEST=" "
ENABLE_PLATFORM_EMBEDDED=" "
EGL_DETECTED=" "
GLESV2_DETECTED=" "
GLEW_DETECTED=" "
WAYLAND_EGL_DETECTED=" "
ENABLE_XDG_V4=" "
ENABLE_XDG_V5=" "

# Checks for library functions.
#Add the subdirectories to be considered for building.
SUBDIRS=" "
#to setup m4 macros
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])],
[AM_DEFAULT_VERBOSITY=1
AC_SUBST(AM_DEFAULT_VERBOSITY)])

PKG_CHECK_MODULES([GLIB],[glib-2.0 >= 2.22.5])
PKG_CHECK_MODULES([GTHREAD],[gthread-2.0 >= 2.38.2])
PKG_CHECK_MODULES([WAYLAND_CLIENT],[wayland-client >= 1.6.0])
PKG_CHECK_MODULES([WAYLAND_SERVER],[wayland-server >= 1.6.0])
PKG_CHECK_MODULES([WAYLAND_EGL],[wayland-egl >= 0.0],[WAYLAND_EGL_DETECTED=true],[WAYLAND_EGL_DETECTED=false])
PKG_CHECK_MODULES([XKBCOMMON],[xkbcommon >= 0.4])
PKG_CHECK_MODULES([EGL],[egl >= 0.0],[EGL_DETECTED=true],[EGL_DETECTED=false])
PKG_CHECK_MODULES([GLESV2],[glesv2 >= 0.0],[GLESV2_DETECTED=true],[GLESV2_DETECTED=false])

AM_CONDITIONAL([HAVE_WAYLAND_EGL], [test x$WAYLAND_EGL_DETECTED = xtrue])              
AM_CONDITIONAL([HAVE_EGL], [test x$EGL_DETECTED = xtrue])              
AM_CONDITIONAL([HAVE_GLESV2], [test x$GLESV2_DETECTED = xtrue])              

AC_ARG_ENABLE([test],
              AS_HELP_STRING([--enable-test],[enable graphics_lifecycle (default is no)]),
              [
                case "${enableval}" in
                 yes) ENABLE_WESTEROS_TEST=true ;;
                  no) AC_MSG_ERROR([graphics_lifecycle is disabled]) ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-test]) ;;
                esac
              ],
              [echo "graphics_lifecycle is disabled"])
AM_CONDITIONAL([ENABLE_WESTEROS_TEST], [test x$ENABLE_WESTEROS_TEST = xtrue])              
AC_ARG_ENABLE([rendergl],
              AS_HELP_STRING([--enable-rendergl],[enable westeros opengl renderer (default is no)]),
              [
                case "${enableval}" in
                 yes) ENABLE_WESTEROS_RENDERERGL=true ;;
                  no) AC_MSG_ERROR([opengl renderer is disabled]) ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-rendergl]) ;;
                esac
              ],
              [echo "westeros opengl renderer is disabled"])
AM_CONDITIONAL([ENABLE_WESTEROS_RENDERERGL], [test x$ENABLE_WESTEROS_RENDERERGL = xtrue])              

AC_ARG_ENABLE([sbprotocol],
              AS_HELP_STRING([--enable-sbprotocol],[enable westeros wl_sb protocol (default is no)]),
              [
                case "${enableval}" in
                 yes) ENABLE_WESTEROS_SBPROTOCOL=true ;;
                  no) AC_MSG_ERROR([westeros wl_sb protocol is disabled]) ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-sbprotocol]) ;;
                esac
              ],
              [echo "westeros wl_sb protocol is disabled"])
AM_CONDITIONAL([ENABLE_WESTEROS_SBPROTOCOL], [test x$ENABLE_WESTEROS_SBPROTOCOL = xtrue])              

AC_ARG_ENABLE([embedded],
              AS_HELP_STRING([--enable-embedded],[enable westeros platform embedded (default is yes)]),
              [
                case "${enableval}" in
                 yes) ENABLE_PLATFORM_EMBEDDED=true ;;
                  no) ENABLE_PLATFORM_EMBEDDED=no ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-embedded]) ;;
                esac
              ],
              [echo "westeros platform embedded is enabled"])
AM_CONDITIONAL([ENABLE_PLATFORM_EMBEDDED], [test x$ENABLE_PLATFORM_EMBEDDED != xno])

AC_ARG_ENABLE([xdgv4],
              AS_HELP_STRING([--enable-xdgv4],[enable xdg_shell protocol v4 (default is no)]),
              [
                case "${enableval}" in
                 yes) ENABLE_XDG_V4=true ENABLE_XDG_V5=false ;;
                  no) AC_MSG_ERROR([xdg_shell protocol v4 is disabled]) ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-xdgv4]) ;;
                esac
              ],
              [echo "xdg_shell protocol v4 is disabled"])
AM_CONDITIONAL([ENABLE_XDG_V4], [test x$ENABLE_XDG_V4 = xtrue])              

AC_ARG_ENABLE([xdgv5],
              AS_HELP_STRING([--enable-xdgv5],[enable xdg_shell protocol v5 (default is no)]),
              [
                case "${enableval}" in
                 yes) ENABLE_XDG_V5=true ENABLE_XDG_V4=false ;;
                  no) AC_MSG_ERROR([xdg_shell protocol v5 is disabled]) ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-xdgv5]) ;;
                esac
              ],
              [echo "xdg_shell protocol v5 is disabled"])
AM_CONDITIONAL([ENABLE_XDG_V5], [test x$ENABLE_XDG_V5 = xtrue])              

WAYLANDLIB="-lwayland-server"
AC_SUBST(WAYLANDLIB)

AC_CONFIG_FILES([Makefile])
AC_SUBST(WAYLAND_CFLAGS)
AC_SUBST(GUPNP_VERSION)
AC_SUBST(ENABLE_WESTEROS_TEST)
AC_OUTPUT

