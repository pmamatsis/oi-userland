#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2013, 2016, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS=NO_ARCH
BUILD_STYLE=setup.py
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		pep8
COMPONENT_VERSION=	1.7.0
COMPONENT_REVISION=	5
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=  http://pypi.python.org/pypi/pep8
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:a113d5f5ad7a7abacef9df5ec3f2af23a20a28005921577b15dd584d099d5900
COMPONENT_ARCHIVE_URL=	http://pypi.python.org/packages/source/p/$(COMPONENT_NAME)/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	python-mod/pep8

PYTHON_VERSIONS=	2.7 3.5

include $(WS_MAKE_RULES)/common.mk

# Replace "#!/usr/bin/env ..." shebang lines with properly versioned ones.
COMPONENT_PRE_BUILD_ACTION = \
	/usr/bin/find $(SOURCE_DIR) -name *.py \
		-exec $(GSED) -i -e 's/env python/python$(PYTHON_VERSION)/' "{}" \; ;

# Put the correct pep8 version number on the .TH line in the man page in
# the proto area.
COMPONENT_POST_INSTALL_ACTION += \
	($(MKDIR) $(PROTO_DIR)/usr/share/man/man1; \
	$(GSED) -e 's/XXX/$(COMPONENT_VERSION)/' \
	    $(COMPONENT_DIR)/files/pep8.1 > \
	    $(PROTO_DIR)/usr/share/man/man1/pep8.1);

COMPONENT_POST_INSTALL_ACTION += \
	(cd $(PROTO_DIR)/usr/bin ; $(MV) -f pep8 pep8-$(PYTHON_VERSION))

# Master test results are the same for all versions of Python, so override
# here, rather than create multiple identical master files.
COMPONENT_TEST_MASTER =	$(COMPONENT_TEST_RESULTS_DIR)/results-all.master

COMPONENT_TEST_DIR =	$(SOURCE_DIR)
COMPONENT_TEST_ARGS =	pep8.py --testsuite testsuite

COMPONENT_SYSTEM_TEST_DIR =	$(SOURCE_DIR)
COMPONENT_SYSTEM_TEST_ENV =
COMPONENT_SYSTEM_TEST_ARGS =	pep8.py --testsuite testsuite

ASLR_MODE = $(ASLR_NOT_APPLICABLE)


# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/setuptools-27
REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-35
