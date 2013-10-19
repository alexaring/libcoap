AC_PREREQ(2.60)
AC_INIT([coap],
        [4.1.1],
        [],
        [coap],
        [http://sourceforge.net/projects/libcoap/])
AC_CONFIG_SRCDIR([src/resource.c])
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([check-news foreign 1.11 -Wall -Wno-portability silent-rules tar-pax no-dist-gzip dist-xz subdir-objects])
AC_PROG_CC_STDC
AC_USE_SYSTEM_EXTENSIONS
AC_SYS_LARGEFILE
AC_CONFIG_MACRO_DIR([m4])
AM_SILENT_RULES([yes])
LT_INIT([disable-static pic-only])
AC_PREFIX_DEFAULT([/usr/local])

AC_PROG_SED
AC_PROG_MKDIR_P

AC_ARG_ENABLE([debug],
        AS_HELP_STRING([--enable-debug], [enable debug messages @<:@default=disabled@:>@]),
        [enable_debug=$enableval], [enable_debug=no])
AS_IF([test "x$enable_debug" = "xno"], [
        AC_DEFINE(NDEBUG, [1], [Debug messages.])
])

AC_ARG_ENABLE([async],
        AS_HELP_STRING([--enable-async], [enable handling of asynchronous transactions and observe @<:@default=enabled@:>@]),
        [enable_async=$enableval], [enable_async=yes])
AS_IF([test "x$enable_async" = "xno"], [
        AC_DEFINE(WITHOUT_ASYNC, [1], [Asynchronous transactions.])
])

AC_ARG_ENABLE([block],
        AS_HELP_STRING([--enable-block], [enable block transfer @<:@default=enabled@:>@]),
        [enable_block=$enableval], [enable_block=yes])
AS_IF([test "x$enable_block" = "xno"], [
        AC_DEFINE(WITHOUT_BLOCK, [1], [Block tansfer.])
])

AC_ARG_ENABLE([observe],
        AS_HELP_STRING([--enable-observe], [enable resource observation @<:@default=enabled@:>@]),
        [enable_observe=$enableval], [enable_observe=yes])
AS_IF([test "x$enable_observe" = "xno"], [
        AC_DEFINE(WITHOUT_OBSERVE, [1], [Resource observation.])
])

AC_ARG_ENABLE([query-filter],
        AS_HELP_STRING([--enable-query-filter], [enable support for filters on /.well-known/core @<:@default=enabled@:>@]),
        [enable_query_filter=$enableval], [enable_query_filter=yes])
AS_IF([test "x$enable_query_filter" = "xno"], [
        AC_DEFINE(WITHOUT_QUERY_FILTER, [1], [Query filter.])
])

AC_ARG_WITH([max-pdu-size],[  --with-max-pdu-size=COAP_MAX_PDU_SIZE Max coap pdu size in bytes @<:@default=1400@:>@],
         [max_pdu_size=$withval], [max_pdu_size=1400])
AS_IF([test "x$max_pdu_size" = "xyes"], [
        AC_MSG_ERROR([The max pdu size must be explicitly specified])
])

AC_DEFINE_UNQUOTED([COAP_MAX_PDU_SIZE], [$max_pdu_size],
		   [Define the max pdu size of a coap pdu in bytes.])


# Checks for header files.
AC_CHECK_HEADERS([assert.h arpa/inet.h limits.h netdb.h netinet/in.h stdlib.h string.h strings.h sys/socket.h sys/time.h time.h unistd.h sys/unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([memset select socket strcasecmp strrchr getaddrinfo strnlen])

libcoap_CFLAGS="-Wall"
AC_SUBST([libcoap_CFLAGS])

AC_CONFIG_HEADERS(config.h)
AC_CONFIG_FILES([
        Makefile
	src/Makefile
	examples/Makefile
])

AC_OUTPUT
AC_MSG_RESULT([
        $PACKAGE $VERSION
        =====

        prefix:                 ${prefix}
        sysconfdir:             ${sysconfdir}
        libdir:                 ${libdir}
        includedir:             ${includedir}

        compiler:               ${CC}
        cflags:                 ${CFLAGS}
        ldflags:                ${LDFLAGS}

	max pdu size:		${max_pdu_size} bytes

        debug:                  ${enable_debug}
        async:                  ${enable_async}
        block:                  ${enable_block}
        observe:                ${enable_observe}
        query-filter:           ${enable_query_filter}
])
