EXTRA_DIST=		libpkg.ver

pkg_common_cflags=	-I$(top_srcdir)/libpkg -I$(top_builddir)/libpkg \
			@LDNS_CFLAGS@ \
			-I$(top_srcdir)/external/libsbuf \
			-I$(top_srcdir)/external/expat/lib \
			-I$(top_srcdir)/external/libucl/include \
			-I$(top_srcdir)/external/picosat \
			-I$(top_srcdir)/external/uthash \
			-I$(top_srcdir)/external/sqlite \
			-I$(top_srcdir)/external/include \
			-DPREFIX=\"$(prefix)\" \
			-Wno-pointer-sign

if LIBELF_BUNDLED
pkg_common_cflags+=	-I$(top_srcdir)/external/libelf
endif

libpkg_la_SOURCES=	pkg.c \
			backup.c \
			dns_utils.c \
			elfhints.c \
			fetch.c \
			packing.c \
			pkg_add.c \
			pkg_attributes.c \
			pkg_audit.c \
			pkg_checksum.c \
			pkg_config.c \
			pkg_cudf.c \
			pkg_create.c \
			pkg_delete.c \
			pkg_elf.c \
			pkg_event.c \
			pkg_jobs.c \
			pkg_jobs_conflicts.c \
			pkg_jobs_universe.c \
			pkg_manifest.c \
			pkg_object.c \
			pkg_ports.c \
			pkg_printf.c \
			pkg_repo.c \
			pkg_repo_create.c \
			pkg_repo_update.c \
			pkg_repo_meta.c \
			pkg_solve.c \
			pkg_status.c \
			pkg_version.c \
			pkgdb.c \
			pkgdb_iterator.c \
			pkgdb_query.c \
			rcscripts.c \
			rsa.c \
			ssh.c \
			scripts.c \
			utils.c \
			plugins.c \
			pkg_old.c \
			merge3.c \
			diff.c
libpkg_la_CFLAGS=	$(pkg_common_cflags) -shared
libpkg_la_LIBADD=	$(top_builddir)/external/libucl.la \
			$(top_builddir)/external/libsqlite.la \
			$(top_builddir)/external/libexpat.la \
			$(top_builddir)/external/libsbuf.la \
			$(top_builddir)/external/libpicosat.la \
			@REPOS_LDADD@ \
			@LIBEXECINFO_LIB@ \
			@LDNS_LIBS@ \
			-larchive \
			-lfetch \
			-lutil \
			-lssl \
			-lcrypto \
			-lm
if LIBELF_BUNDLED
libpkg_la_LIBADD+=	$(top_builddir)/external/libelf.la
else
libpkg_la_LIBADD+=	-lelf
endif

libpkg_la_LDFLAGS=	-version-info @LIBPKG_SO_VERSION@ -Wl,--version-script=$(srcdir)/libpkg.ver
EXTRA_libpkg_la_DEPENDENCIES=	@REPOS_LDADD@ libpkg.ver

DYNLIBS=		libpkg.la
lib_LTLIBRARIES=	libpkg_static.la
if DYNAMIC
lib_LTLIBRARIES+=	$(DYNLIBS)
endif
include_HEADERS=	pkg.h

libpkg_static_la_SOURCES=	$(libpkg_la_SOURCES)
libpkg_static_la_CFLAGS=	$(pkg_common_cflags) -static
libpkg_static_la_LIBADD=	$(top_builddir)/external/libucl_static.la \
			$(top_builddir)/external/libsqlite_static.la \
			$(top_builddir)/external/libexpat_static.la \
			$(top_builddir)/external/libpicosat_static.la \
			$(top_builddir)/external/libsbuf_static.la \
			@REPOS_LDADD_STATIC@

EXTRA_libpkg_static_la_DEPENDENCIES=	@REPOS_LDADD_STATIC@ libpkg.ver

libpkg_static_la_LDFLAGS=	-all-static

noinst_HEADERS=		private/db_upgrades.h \
			private/elf_tables.h \
			private/event.h \
			private/ldconfig.h \
			private/pkg.h \
			private/pkg_printf.h \
			private/pkgdb.h \
			private/utils.h \
			private/pkg_jobs.h

SUBDIRS = repo .
