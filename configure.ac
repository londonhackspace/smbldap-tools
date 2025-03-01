## smbldap-tools configure.in
## ======================================================================

AC_PREREQ([2.71])

AC_INIT([smbldap-tools],[0.9.11])

AC_PREFIX_DEFAULT(/usr/local)

#AC_PROG_INSTALL

package_subdir="$PACKAGE_NAME"
PERL_VERSION=5.008001
SAMBA_SYSCONFDIR="/etc/samba"
SAMBA_BINDIR="/usr/bin"

AC_CONFIG_FILES(
    Makefile
    build/Makefile.common
    build/Makefile.package
    build/Makefile.top
    build/subst.pl
    build/subst.vars
)

## Installation directories
## ======================================================================

AC_SUBST(package_subdir)

AC_ARG_WITH(
  subdir,
  [AS_HELP_STRING([--with-subdir=DIR],[change default subdirectory used for installs])],
  [package_subdir="$withval"],
)

case "$package_subdir" in
yes|no|"")
    package_subdir=""
    ;;
*)
    AC_MSG_RESULT([using $package_subdir for install subdir])
    package_subdir="/$package_subdir"
    ;;
esac

## Perl
## ======================================================================

AC_SUBST(PERL_COMMAND)

AC_ARG_WITH(
    perl,
    [AS_HELP_STRING([--with-perl=PATH],[Use specific perl command])],
    [PERL_COMMAND="$withval"],
)

case "$PERL_COMMAND" in
/*)
    ;;
*)
    AC_PATH_PROG(PERL_COMMAND, perl)
    ;;
esac

AC_MSG_RESULT([using $PERL_COMMAND for perl command])

## ----------------------------------------------------------------------

AC_MSG_CHECKING(for Perl version)

if test x`"$PERL_COMMAND" -e "use $PERL_VERSION; print 'ok'"` = x"ok"; then
    AC_MSG_RESULT($PERL_VERSION or later)
else
    AC_MSG_ERROR(Perl $PERL_VERSION or later required.)
fi

## ----------------------------------------------------------------------

AC_MSG_CHECKING(for Perl Digest::SHA1 or Digest::SHA)
AC_SUBST(PERL_DIGEST_SHA)

if test x`"$PERL_COMMAND" -e "use 5.010000; print 'ok'" 2>/dev/null` = x"ok"; then
    PERL_DIGEST_SHA="Digest::SHA"
else
    PERL_DIGEST_SHA="Digest::SHA1"
fi

AC_MSG_RESULT([$PERL_DIGEST_SHA])

## ----------------------------------------------------------------------

AC_SUBST(PERL_LIBDIR)

AC_ARG_WITH(
    perl-libdir,
    [AS_HELP_STRING([--with-perl-libdir=PATH],[*.pm install directory])],
    [PERL_LIBDIR="$withval"],
)

case "$PERL_LIBDIR" in
/*)
    ;;
sitelib)
    PERL_LIBDIR=`$PERL_COMMAND -MConfig -e 'print $Config{installsitelib}'`
    ;;
*)
    PERL_LIBDIR=`$PERL_COMMAND -MConfig -e 'print $Config{installvendorlib}'`
    ;;
esac

AC_MSG_RESULT([using $PERL_LIBDIR for *.pm install directory])

## ----------------------------------------------------------------------

AC_SUBST(POD2MAN_COMMAND)

AC_ARG_WITH(
    pod2man,
    [AS_HELP_STRING([--with-pod2man=PATH],[Use specific pod2man command])],
    [POD2MAN_COMMAND="$withval"],
)

case "$POD2MAN_COMMAND" in
/*)
    ;;
*)
    AC_PATH_PROG(POD2MAN_COMMAND, pod2man)
    ;;
esac

AC_MSG_RESULT([using $POD2MAN_COMMAND for pod2man command])

## Samba
## ======================================================================

AC_SUBST(SAMBA_SYSCONFDIR)

AC_ARG_WITH(
    samba-sysconfdir,
    [AS_HELP_STRING([--with-samba-sysconfdir=DIR],[Path for Samba sysconf directory])],
    [SAMBA_SYSCONFDIR="$withval"],
)

AC_MSG_RESULT([using $SAMBA_SYSCONFDIR for Samba sysconf directory])

## ----------------------------------------------------------------------

AC_SUBST(SAMBA_BINDIR)

AC_ARG_WITH(
    samba_bindir,
    [AS_HELP_STRING([--with-samba-bindir=DIR],[Path for Samba bin directory])],
    [SAMBA_BINDIR="$withval"],
)

AC_MSG_RESULT([using $SAMBA_BINDIR for Samba bin directory])

## Output
## ======================================================================

AC_OUTPUT

