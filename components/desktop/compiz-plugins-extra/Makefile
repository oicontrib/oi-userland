#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2014 Alexander Pyhalov
# Copyright (c) 2018 Michal Nowak
#

BUILD_BITS=	64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		compiz-plugins-extra
COMPONENT_VERSION=	0.8.16
COMPONENT_PROJECT_URL=	http://www.northfield.ws/
COMPONENT_SUMMARY=	extra effects plugins for compiz
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_NAME)-$(COMPONENT_VERSION).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:e942ffe0549bf1935c4a69eafea5b888c2646e198cb94e023d373b8d47c0cfa3
COMPONENT_ARCHIVE_URL=	http://www.northfield.ws/projects/compiz/releases/$(COMPONENT_VERSION)/$(COMPONENT_SRC).tar.xz

TEST_TARGET = $(NO_TESTS)

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

COMPONENT_PREP_ACTION = ( cd $(@D) && \
	aclocal -I. && \
	autoheader && \
	libtoolize --automake --copy --force && \
	automake -a -f -c &&\
	autoconf &&\
	find $(@D) -name '*_options.c' -o -name '*_options.h' -exec rm -f {} \; )

CONFIGURE_ENV+=	INTLTOOL_PERL=$(PERL)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--disable-static

# Build dependencies
REQUIRED_PACKAGES += desktop/compiz/bcop
REQUIRED_PACKAGES += desktop/compiz/plugin/compiz-fusion-main

# Auto-generated dependencies
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libnotify
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += x11/library/glu
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxext
REQUIRED_PACKAGES += x11/library/libxfixes
