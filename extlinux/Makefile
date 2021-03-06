## -----------------------------------------------------------------------
##
##   Copyright 2001-2008 H. Peter Anvin - All Rights Reserved
##
##   This program is free software; you can redistribute it and/or modify
##   it under the terms of the GNU General Public License as published by
##   the Free Software Foundation, Inc., 53 Temple Place Ste 330,
##   Boston MA 02111-1307, USA; either version 2 of the License, or
##   (at your option) any later version; incorporated herein by reference.
##
## -----------------------------------------------------------------------

##
## Linux vfat, ntfs, ext2/ext3/ext4 and btrfs installer
##

include $(MAKEDIR)/syslinux.mk

OPTFLAGS = -g -Os
INCLUDES = -I$(SRC) -I$(objdir) -I$(SRC)/../libinstaller
CFLAGS	 = $(CFLAGS_FOR_BUILD) $(GCCWARN) -Wno-sign-compare -D_FILE_OFFSET_BITS=64 \
	   $(OPTFLAGS) $(INCLUDES)
LDFLAGS	 = $(LDFLAGS_FOR_BUILD)

SRCS     = main.c \
	   mountinfo.c \
	   ../libinstaller/syslxmod.c \
	   ../libinstaller/syslxopt.c \
	   ../libinstaller/syslxcom.c \
	   ../libinstaller/setadv.c \
	   ../libinstaller/advio.c \
	   ../libinstaller/bootsect_bin.c \
	   ../libinstaller/ldlinuxc32_bin.c \
	   ../libinstaller/ldlinux_bin.c
OBJS	 = $(patsubst %.c,%.o,$(notdir $(SRCS)))

.SUFFIXES: .c .o .i .s .S

VPATH = $(SRC):$(SRC)/../libinstaller:$(OBJ)/../libinstaller

all: installer

tidy dist:
	-rm -f *.o *.i *.s *.a .*.d *.tmp

clean: tidy
	-rm -f extlinux

spotless: clean
	-rm -f *~

installer: extlinux

extlinux: $(OBJS)
	$(CC_FOR_BUILD) $(LDFLAGS) -o $@ $^

strip:
	$(STRIP) extlinux

%.o: %.c
	$(CC_FOR_BUILD) $(UMAKEDEPS) $(CFLAGS) -c -o $@ $<
%.i: %.c
	$(CC_FOR_BUILD) $(UMAKEDEPS) $(CFLAGS) -E -o $@ $<
%.s: %.c
	$(CC_FOR_BUILD) $(UMAKEDEPS) $(CFLAGS) -S -o $@ $<

-include .*.d
