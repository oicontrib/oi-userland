#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2020 Evgeny Litvinenko
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		wine
COMPONENT_VERSION=	5.2
COMPONENT_PROJECT_URL=	https://www.winehq.org/
COMPONENT_SUMMARY=	Wine - Run Windows applications.
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:c10c9c34f0eade1d1063ce983e6f1ad8904c9cb604d8fea4df5e1cefdba85d40
COMPONENT_ARCHIVE_URL=	https://dl.winehq.org/wine/source/4.x/$(COMPONENT_ARCHIVE)
COMPONENT_SIG_URL=	$(COMPONENT_ARCHIVE_URL).sign
COMPONENT_FMRI=		runtime/wine
COMPONENT_LICENSE=	LGPLv2.1
COMPONENT_LICENSE_FILE=	$(COMPONENT_NAME).license
COMPONENT_CLASSIFICATION=	Applications/System Utilities

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH= $(PATH.gnu)

COMPONENT_PREP_ACTION = ( cd $(@D) && autoreconf -f --install )

CONFIGURE_PREFIX  = /opt/wine
CONFIGURE_OPTIONS += AS="/usr/bin/gas"
CONFIGURE_OPTIONS += --with-pulse
CONFIGURE_OPTIONS += --with-oss
CONFIGURE_OPTIONS += LDAP_CFLAGS="-I/usr/include/openldap"

ELFEDIT=/usr/bin/elfedit
WINE_EXE= wine
WINE_LIB= libwine.so.1.0
WINE_ADD_EXE= widl winebuild winecpp winedump wineg++ winegcc \
	      wineserver wmc wrc

FINAL_TRANSFORMS += depend_facets

COMPONENT_POST_INSTALL_ACTION = \
	for file in $(WINE_EXE) ; \
	do \
	    $(ELFEDIT) -e 'dyn:delete RUNPATH' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/bin/$$file; \
	    $(ELFEDIT) -e 'dyn:value  -s RPATH "$$ORIGIN/../lib"' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/bin/$$file; \
	done; \
	for file in $(WINE_ADD_EXE) ; \
	do \
	    $(ELFEDIT) -e 'dyn:delete RUNPATH' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/bin/$$file; \
	    $(ELFEDIT) -e 'dyn:delete RPATH' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/bin/$$file; \
	done; \
	for file in $(WINE_LIB) ; \
	do \
	    $(ELFEDIT) -e 'dyn:delete RUNPATH' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/lib/$$file; \
	    $(ELFEDIT) -e 'dyn:delete RPATH' $(PROTO_DIR)/$(CONFIGURE_PREFIX)/lib/$$file; \
	done; \
	for file in $(PROTO_DIR)/$(CONFIGURE_PREFIX)/lib/wine/*.so ; \
	do \
	    $(ELFEDIT) -e 'dyn:delete RUNPATH' $$file; \
	    $(ELFEDIT) -e 'dyn:value  -s RPATH "$$ORIGIN/.."' $$file; \
	done;

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TEST)

# Auto-generated dependencies
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += audio/mpg123
REQUIRED_PACKAGES += library/audio/gstreamer1
REQUIRED_PACKAGES += library/audio/gstreamer1/plugin/base
REQUIRED_PACKAGES += library/audio/openal
REQUIRED_PACKAGES += library/audio/pulseaudio
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/lcms2
REQUIRED_PACKAGES += library/libgphoto2-2
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/openldap
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/perl-524
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/libpcap
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxext
