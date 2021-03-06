#
# src/swtpm/Makefile.am
#
# For the license, see the COPYING file in the root directory.
#

noinst_HEADERS = \
	common.h \
	ctrlchannel.h \
	key.h \
	locality.h \
	logging.h \
	main.h \
	mainloop.h \
	options.h \
	pidfile.h \
	server.h \
	swtpm_aes.h \
	swtpm_debug.h \
	swtpm_io.h \
	swtpm_nvfile.h \
	threadpool.h \
	tlv.h \
	tpmlib.h \
	tpmstate.h \
	utils.h \
	vtpm_proxy.h

lib_LTLIBRARIES = libswtpm_libtpms.la

libswtpm_libtpms_la_SOURCES = \
	common.c \
	ctrlchannel.c \
	key.c \
	logging.c \
	mainloop.c \
	options.c \
	pidfile.c \
	server.c \
	swtpm_aes.c \
	swtpm_debug.c \
	swtpm_io.c \
	swtpm_nvfile.c \
	tlv.c \
	tpmlib.c \
	tpmstate.c \
	threadpool.c \
	utils.c

libswtpm_libtpms_la_CFLAGS = \
	-I$(top_srcdir)/include/swtpm \
	$(HARDENING_CFLAGS) \
	$(GLIB_CFLAGS)

libswtpm_libtpms_la_LIBADD = \
	$(LIBTPMS_LIBS) \
	$(GLIB_LIBS)

bin_PROGRAMS = swtpm
if WITH_CUSE
bin_PROGRAMS += swtpm_cuse
endif

swtpm_DEPENDENCIES = $(lib_LTLIBRARIES)

swtpm_SOURCES = \
		main.c \
		swtpm.c \
		swtpm_chardev.c
if WITH_CUSE
swtpm_SOURCES += cuse_tpm.c
endif

swtpm_CFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/include/swtpm \
	$(HARDENING_CFLAGS) \
	$(GLIB_CFLAGS) \
	$(LIBFUSE_CFLAGS) \
	-DHAVE_SWTPM_CUSE_MAIN

swtpm_LDADD = \
	-L$(PWD)/.libs -lswtpm_libtpms \
	$(LIBFUSE_LIBS) \
	$(GLIB_LIBS) \
	$(GTHREAD_LIBS) \
	$(LIBTPMS_LIBS)

swtpm_cuse_DEPENDENCIES = $(lib_LTLIBRARIES)

swtpm_cuse_SOURCES = \
	cuse_tpm.c

swtpm_cuse_CFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/include/swtpm \
	$(GLIB_CFLAGS) \
	$(LIBFUSE_CFLAGS) \
	$(HARDENING_CFLAGS)

swtpm_cuse_LDADD = \
	-L$(PWD)/.libs -lswtpm_libtpms \
	$(LIBFUSE_LIBS) \
	$(GLIB_LIBS) \
	$(GTHREAD_LIBS) \
	$(LIBTPMS_LIBS)

AM_CPPFLAGS   = 
LDADD         = -ltpms
