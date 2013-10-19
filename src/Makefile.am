EXTRA_DIST =
CLEANFILES =

AM_CFLAGS = \
        -include $(top_builddir)/config.h \
	-DSYSCONFDIR=\""$(sysconfdir)"\" \
	-DLIBEXECDIR=\""$(libexecdir)"\" \
	-I${top_srcdir}/src/coap \
	${libcoap_CFLAGS} \
	-ffunction-sections \
	-fdata-sections

AM_LDFLAGS = \
	-Wl,--gc-sections \
	-Wl,--as-needed

SED_PROCESS = \
	$(AM_V_GEN)$(MKDIR_P) $(dir $@) && $(SED) \
	-e 's,@VERSION\@,$(VERSION),g' \
	-e 's,@prefix\@,$(prefix),g' \
	-e 's,@exec_prefix\@,$(exec_prefix),g' \
	-e 's,@libdir\@,$(libdir),g' \
	-e 's,@includedir\@,$(includedir)/coap,g' \
	< $< > $@ || rm $@

%.pc: %.pc.in Makefile
	$(SED_PROCESS)

LIBCOAP_CURRENT=4
LIBCOAP_REVISION=0
LIBCOAP_AGE=3

pkginclude_HEADERS =\
	coap/address.h \
	coap/async.h \
	coap/bits.h \
	coap/block.h \
	coap/coap.h \
	coap/coap_list.h \
	coap/coap_time.h \
	coap/debug.h \
	coap/encode.h \
	coap/hashkey.h \
	coap/mem.h \
	coap/net.h \
	coap/option.h \
	coap/pdu.h \
	coap/prng.h \
	coap/resource.h \
	coap/str.h \
	coap/subscribe.h \
	coap/t_list.h \
	coap/uri.h \
	coap/uthash.h \
	coap/utlist.h

lib_LTLIBRARIES = libcoap.la

libcoap_la_SOURCES =\
	async.c \
	block.c \
	coap_list.c \
	debug.c \
	encode.c \
	hashkey.c \
	net.c \
	option.c \
	pdu.c \
	resource.c \
	str.c \
	subscribe.c \
	uri.c

libcoap_la_LDFLAGS = $(AM_LDFLAGS) \
	-version-info $(LIBCOAP_CURRENT):$(LIBCOAP_REVISION):$(LIBCOAP_AGE)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libcoap.pc
EXTRA_DIST += libcoap.pc.in
CLEANFILES += libcoap.pc
