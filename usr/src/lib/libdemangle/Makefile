#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#
# Copyright 2018 Jason King.
# Copyright 2017, Joyent. Inc.
#

include		../Makefile.lib

HDRS =			demangle-sys.h
HDRDIR =		common
SUBDIRS =		$(MACH)
$(BUILD64)SUBDIRS +=	$(MACH64)

all :=		TARGET= all
clean :=	TARGET= clean
clobber :=	TARGET= clobber
install :=	TARGET= install
lint :=		TARGET= lint

.KEEP_STATE:

all clean clobber install lint: $(SUBDIRS)

$(SUBDIRS):	FRC
	@cd $@; pwd; $(MAKE) $(TARGET)

install_h:	$(ROOTHDRS)

check:		$(CHECKHDRS)

FRC:

include ../Makefile.targ
