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
# Copyright 2016-2018 Aurelien Larcher
#
PREFERRED_BITS=64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         hwloc
COMPONENT_VERSION_MAJOR=2.0
COMPONENT_VERSION=      $(COMPONENT_VERSION_MAJOR).1
COMPONENT_SUMMARY=      hwloc - Portable Hardware Locality
COMPONENT_PROJECT_URL=  https://www.open-mpi.org/projects/hwloc/
COMPONENT_FMRI=         developer/hwloc
COMPONENT_CLASSIFICATION=Development/High Performance Computing
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_URL= \
  https://www.open-mpi.org/software/hwloc/v$(COMPONENT_VERSION_MAJOR)/downloads/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= \
  sha256:b97575cc26751f252b5c9f5c00be94cab66977da2e127456a5ae2418649ec049
COMPONENT_LICENSE=      BSD-2

# When CONFIGURE_FIX_LIBTOOL_RPATH is integrated, we can remove local fix and enable it
CONFIGURE_FIX_LIBTOOL_RPATH = no

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

CONFIGURE_OPTIONS+= --enable-cairo
CONFIGURE_OPTIONS+= --enable-cpuid
CONFIGURE_OPTIONS+= --enable-libxml2
CONFIGURE_OPTIONS+= --enable-pci

CONFIGURE_ENV.64 += LT_SYS_LIBRARY_PATH="/lib/$(MACH64):/usr/lib/$(MACH64)"

unexport SHELLOPTS
COMPONENT_TEST_TRANSFORMS += \
        '-n ' \
        '-e "/TOTAL:/p" ' \
        '-e "/SKIP:/p" ' \
        '-e "/PASS:/p" ' \
        '-e "/FAIL:/p" ' \
        '-e "/ERROR:/p" '

build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

test:		$(TEST_32_and_64)

# Build dependencies
REQUIRED_PACKAGES += system/header/header-picl

# Auto-generated dependencies
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += diagnostic/scanpci
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += service/picl
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
