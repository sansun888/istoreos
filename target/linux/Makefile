# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2006-2007 OpenWrt.org

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/target.mk

export TARGET_BUILD=1

prereq clean download prepare compile install oldconfig menuconfig nconfig xconfig update refresh image: darwin FORCE
	@+$(NO_TRACE_MAKE) -C $(BOARD) $@

.PHONY: darwin
darwin: $(STAGING_DIR_HOST)/include/asm/.ready

ifeq ($(HOST_OS),Darwin)
$(STAGING_DIR_HOST)/include/asm/.ready: $(STAGING_DIR_HOST)/include/asm/types.h $(STAGING_DIR_HOST)/include/asm/posix_types.h
	touch $(STAGING_DIR_HOST)/include/asm/.ready
else
$(STAGING_DIR_HOST)/include/asm/.ready:
	mkdir -p $(STAGING_DIR_HOST)/include/asm
	echo 'Not darwin' > $(STAGING_DIR_HOST)/include/asm/.ready
endif

$(STAGING_DIR_HOST)/include/asm/types.h: Makefile
	mkdir -p $(STAGING_DIR_HOST)/include/asm
	echo '// auto generated by target/linux/Makefile, for macos host build tools'  >  $@
	echo '#ifndef __ASM_TYPES_H'  >>  $@
	echo '#define __ASM_TYPES_H'  >>  $@
	echo '#include <stdint.h>'  >>  $@
	$(foreach bw, 8 16 32 64,\
	echo 'typedef uint$(bw)_t __u$(bw);' >> $@ ; \
	echo 'typedef int$(bw)_t __s$(bw);' >> $@ ; \
	) 
	echo '#endif'  >>  $@

$(STAGING_DIR_HOST)/include/asm/posix_types.h: Makefile
	mkdir -p $(STAGING_DIR_HOST)/include/asm
	touch $@
