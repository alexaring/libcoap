AM_LDFLAGS = $(top_builddir)/src/libcoap.la
AM_CFLAGS = -I $(top_builddir)/src/coap -include $(top_builddir)/config.h

bin_PROGRAMS = \
	coap-client \
	coap-server

coap_client_SOURCES = client.c
coap_server_SOURCES = server.c
