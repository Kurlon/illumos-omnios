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
# Copyright 2010 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
# Copyright 2019 Joyent, Inc.
# Copyright 2019 OmniOS Community Edition (OmniOSce) Association.
#

PROG= profile .login ksh.kshrc system
PROGSKEL= .profile .kshrc
PROGROOT= .profile .bashrc

include ../Makefile.cmd

ROOTROOT= $(ROOT)/root
ROOTETCSKEL= $(ROOTETC)/skel
ROOTETCSKELPROG= $(PROGSKEL:%=$(ROOTETCSKEL)/%)
ROOTETCVERSIONS= $(ROOTETC)/versions
ROOTETCVERSIONSPROG= $(ROOTETCVERSIONS)/build
ROOTETCVERSIONSPROGPROJECT= $(ROOTETCVERSIONSPROG).$(PROJECT)
ROOTROOTPROG= $(PROGROOT:%=$(ROOTROOT)/%)
FILEMODE= 0644

CLOBBERFILES = profile .bashrc .profile .login .kshrc

.login: login.csh
	$(RM) .login
	$(CP) login.csh .login

profile: etc-profile.sh
	$(RM) profile
	$(CP) etc-profile.sh $@

.profile: dot-profile.sh
	$(RM) .profile
	$(CP) dot-profile.sh $@

.kshrc: dot-kshrc.sh
	$(RM) .kshrc
	$(CP) dot-kshrc.sh $@

.bashrc: bashrc.sh
	$(RM) .bashrc
	$(CP) bashrc.sh $@

.KEEP_STATE:

all: $(PROG) $(PROGSKEL)

$(ROOTROOT)/% \
$(ROOTETCSKEL)/%: %
	$(INS.file)

$(ROOTROOT) \
$(ROOTETCVERSIONS) \
$(ROOTETCSKEL):
	$(INS.dir)

$(ROOTETCVERSIONSPROG): $(ROOTETCVERSIONS) FRC
	if [[ -n "$$BUILDVERSION_EXEC" ]]; then \
		$$BUILDVERSION_EXEC >$(ROOTETCVERSIONSPROG) ; \
	else \
		touch $(ROOTETCVERSIONSPROG) ; \
	fi

$(ROOTETCVERSIONSPROGPROJECT): $(ROOTETCVERSIONSPROG) FRC
	$(CP) $(ROOTETCVERSIONSPROG) $(ROOTETCVERSIONSPROGPROJECT)

install: all $(ROOTETCSKEL) $(ROOTETCPROG) \
    $(ROOTETCSKELPROG) $(ROOTROOTPROG) \
    $(ROOTETCVERSIONSPROG) $(ROOTETCVERSIONSPROGPROJECT)

clean:

clobber:
	$(RM) $(CLOBBERFILES)

FRC:
