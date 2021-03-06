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
# Copyright (c) 2005, 2010, Oracle and/or its affiliates. All rights reserved.
# Copyright 2015, OmniTI Computer Consulting, Inc. All rights reserved.
# Copyright 2018 OmniOS Community Edition (OmniOSce) Association.
#

include		$(SRC)/data/Makefile.data

HWDATA=		pci.ids usb.ids efi.fixes
HWDATADIR=	$(ROOT)/usr/share/hwdata
ROOTHWDATA=	$(HWDATA:%=$(HWDATADIR)/%)

CLOBBERFILES=	THIRDPARTYLICENSE.pciids THIRDPARTYLICENSE.efifixes

$(ROOTHWDATA):=	FILEMODE = 444

all install:	THIRDPARTYLICENSE.pciids THIRDPARTYLICENSE.efifixes

THIRDPARTYLICENSE.pciids: pci.ids THIRDPARTYLICENSE.pciids.tmpl
		$(RM) $@
		$(SED) -e '/^$$/,$$ d' < pci.ids > $@
		$(CAT) THIRDPARTYLICENSE.pciids.tmpl >> $@

THIRDPARTYLICENSE.efifixes: efi.fixes THIRDPARTYLICENSE.efifixes.tmpl
		$(RM) $@
		$(SED) -e '/^$$/,$$ d' < efi.fixes > $@
		$(CAT) THIRDPARTYLICENSE.efifixes.tmpl >> $@

install:	$(ROOTHWDATA)

$(HWDATADIR)/%: %
		$(INS.file)

clean:

# The "update" target family allows a simple pull-from-the-source update.
# One can then use revision-control diffs to see what actually changed.
update:		usb.update pci.update

# URLs for PCI IDs and USB IDs
PCIURL=		http://pci-ids.ucw.cz/v2.2/pci.ids
USBURL=		http://www.linux-usb.org/usb.ids

# These could move into Makefile.master
URL_FETCH=	wget
URL_FETCHARGS=

pci.update:
		$(RM) pci.ids
		$(URL_FETCH) $(URL_FETCHARGS) $(PCIURL)

usb.update:
		$(RM) usb.ids
		$(URL_FETCH) $(URL_FETCHARGS) $(USBURL)

include		$(SRC)/data/Makefile.targ
