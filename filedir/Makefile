ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "linux"
	ZAP = zap
else
	ZAP =
endif

PROGS = access cdpwd changemod devrdev filetype mycd umask unlink $(ZAP)
MOREPROGS = ftw8

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS) $(MOREPROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/ftw8: ftw8.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $(NAMEMAX) ftw8.c -o $@ $(LDFLAGS) $(LDLIBS)

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
