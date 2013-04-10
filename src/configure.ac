#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(Deep Space Window Manager, esyscmd(grep :version dswm.asd | cut -d\" -f2 | tr -d \\n), esyscmd(grep :author dswm.asd | cut -d\< -f2 | cut -d\> -f1 | tr -d \\n))

AC_SUBST(MAKE_ALL_DEPS)
AC_SUBST(MAKE_INSTALL_DEPS)
AC_SUBST(MAKE_UNINSTALL_DEPS)
AC_SUBST(MODULES_DIR)
AC_SUBST(LISP)
AC_SUBST(LISP_PROGRAM)
AC_SUBST(DSWM_BIN_DIR)

# Checks for programs.
AC_ARG_WITH(lisp, [ --with-lisp=IMPL use the specified lisp (sbcl, cmucl, clisp, ccl, ecl or lw)], LISP=$withval, LISP="any")
AC_ARG_WITH(sbcl, [ --with-sbcl=PATH specify location of sbcl], SBCL_PATH=$withval, SBCL_PATH="")
AC_ARG_WITH(cmucl, [ --with-cmucl=PATH specify location of cmucl], CMUCL_PATH=$withval, CMUCL_PATH="")
AC_ARG_WITH(clisp, [ --with-clisp=PATH specify location of clisp], CLISP_PATH=$withval, CLISP_PATH="")
AC_ARG_WITH(ccl, [ --with-ccl=PATH specify location of ccl], CCL_PATH=$withval, CCL_PATH="")
AC_ARG_WITH(ecl, [ --with-ecl=PATH specify location of ecl], ECL_PATH=$withval, ECL_PATH="")
AC_ARG_WITH(lw, [ --with-lw=PATH specify location of lispworks], LW_PATH=$withval, LW_PATH="")
AC_ARG_WITH(manual, [  --with-manual compile with manual for DSWM (need cl-ppcre)], MANUALP="true", MANUALP="")
AC_ARG_WITH(gnome, [  --with-gnome-session add DSWM session with gnome desktop environment], GNOMEP="true", GNOMEP="")
AC_ARG_WITH(mate, [  --with-mate-session add DSWM session with mate desktop environment], MATEP="true", MATEP="")
AC_ARG_WITH(unity, [  --with-unity-session add DSWM session with unity desktop environment], UNITYP="true", UNITYP="")
AC_ARG_WITH(kde, [  --with-kde-session add DSWM session with KDE desktop environment], KDEP="true", KDEP="")
AC_ARG_WITH(xfce, [  --with-xfce-session add DSWM session with XFCE desktop environment], XFCEP="true", XFCEP="")

if test -x "$SBCL_PATH"; then
   SBCL=$SBCL_PATH
   AC_MSG_CHECKING([for sbcl])
   AC_MSG_RESULT($SBCL)
else
   AC_PATH_PROG([SBCL], sbcl,"")
fi

if test -x "$CMUCL_PATH"; then
   CMUCL=$CMUCL_PATH
   AC_MSG_CHECKING([for cmucl])
   AC_MSG_RESULT($CMUCL)
else
   AC_PATH_PROG([CMUCL], cmucl,"")
fi

if test -x "$CLISP_PATH"; then
   CLISP=$CLISP_PATH
   AC_MSG_CHECKING([for clisp])
   AC_MSG_RESULT($CLISP)
else
   AC_PATH_PROG([CLISP],clisp,"")
fi

if test -x "$CCL_PATH"; then
   CCL=$CCL_PATH
   AC_MSG_CHECKING([for ccl])
   AC_MSG_RESULT($CCL)
else
   AC_PATH_PROG([CCL],ccl,"")
fi

if test -x "$ECL_PATH"; then
   ECL=$ECL_PATH
   AC_MSG_CHECKING([for ecl])
   AC_MSG_RESULT($ECL)
else
   AC_PATH_PROG([ECL], ecl,"")
fi

if test -x "$LW_PATH"; then
   LW=$LW_PATH
   AC_MSG_CHECKING([for lispworks])
   AC_MSG_RESULT($LW)
else
   AC_PATH_PROG([LW], lw,"")
fi

if test "x$LISP" = "xany"; then
   if test "$SBCL"; then
      LISP=sbcl
   elif test "$CMUCL"; then
      LISP=cmucl
   elif test "$CLISP"; then
      LISP=clisp
   elif test "$CCL"; then
      LISP=ccl
   elif test "$ECL"; then
      LISP=ecl
   elif test "$LW"; then
      LISP=lw
   fi
fi

if test "x$LISP" = "xsbcl"; then
   LISP_PROGRAM=$SBCL
elif test "x$LISP" = "xcmucl"; then
   LISP_PROGRAM=$CMUCL
elif test "x$LISP" = "xclisp"; then
   LISP_PROGRAM=$CLISP
elif test "x$LISP" = "xccl"; then
   LISP_PROGRAM=$CCL
elif test "x$LISP" = "xecl"; then
   LISP_PROGRAM=$ECL
elif test "x$LISP" = "xlw"; then
   LISP_PROGRAM=$LW
fi

if test "x$LISP_PROGRAM" = "x"; then
   AC_MSG_ERROR([*** No lisp is available.])
fi

AC_MSG_NOTICE([Using $LISP at $LISP_PROGRAM])

# check for makeinfo
if test "x$MANUALP" = "true"; then
   MAKE_ALL_DEPS="dswm dswm.info"
   MAKE_INSTALL_DEPS="dswm.install dswm.info.install"

   # check for makeinfo
   AC_CHECK_PROG(MAKEINFO,makeinfo,yes,no)
   if test "$MAKEINFO" = "no"; then
      AC_MSG_ERROR([*** Please install makeinfo for the manual.])
   fi
else
   MAKE_ALL_DEPS="dswm"
   MAKE_INSTALL_DEPS="dswm.install"
   MAKE_UNINSTALL_DEPS="dswm.uninstall"
fi

if test "x$GNOMEP" = "true"; then
   MAKE_ALL_DEPS="$MAKE_ALL_DEPS dswm.gnome"
   MAKE_INSTALL_DEPS="$MAKE_INSTALL_DEPS dswm.gnome.install"
   MAKE_INSTALL_DEPS="$MAKE_UNINSTALL_DEPS dswm.gnome.uninstall"
fi

if test "x$MATEP" = "true"; then
   MAKE_ALL_DEPS="$MAKE_ALL_DEPS dswm.mate"
   MAKE_INSTALL_DEPS="$MAKE_INSTALL_DEPS dswm.mate.install"
   MAKE_UNINSTALL_DEPS="$MAKE_UNINSTALL_DEPS dswm.mate.uninstall"
fi

if test "x$UNITYP" = "true"; then
   MAKE_ALL_DEPS="$MAKE_ALL_DEPS dswm.unity"
   MAKE_INSTALL_DEPS="$MAKE_INSTALL_DEPS dswm.unity.install"
   MAKE_UNINSTALL_DEPS="$MAKE_UNINSTALL_DEPS dswm.unity.uninstall"
fi

if test "x$KDEP" = "true"; then
   MAKE_ALL_DEPS="$MAKE_ALL_DEPS dswm.kde"
   MAKE_INSTALL_DEPS="$MAKE_INSTALL_DEPS dswm.kde.install"
   MAKE_UNINSTALL_DEPS="$MAKE_UNINSTALL_DEPS dswm.kde.uninstall"
fi

if test "x$XFCEP" = "true"; then
   MAKE_ALL_DEPS="$MAKE_ALL_DEPS dswm.xfce"
   MAKE_INSTALL_DEPS="$MAKE_INSTALL_DEPS dswm.xfce.install"
   MAKE_UNINSTALL_DEPS="$MAKE_UNINSTALL_DEPS dswm.xfce.uninstall"
fi

AC_CHECK_PROG(XDPYINFO,xdpyinfo,yes,no)
if test "$XDPINFO" = "no"; then
   AC_MSG_WARN([xdpyinfo is needed for xinerama support.])
fi

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.
AC_OUTPUT(Makefile)
AC_OUTPUT(module.lisp)
AC_OUTPUT(help.lisp)
AC_OUTPUT(../config/dswm.desktop)
AC_OUTPUT(../doc/dswm.texi)
