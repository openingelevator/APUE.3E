ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "linux"
  EXTRALIBS=-lrt
endif
ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lrt
endif

PROGS = deadlock mandatory mcopy2 nonblockw rot13a
MOREPROGS = rot13c2

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/rot13c2 $(BUILD_DIR)/lockfile.o

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/xlate: rot13a.c $(LIBAPUE) | $(BUILD_DIR)
	./fixup.awk rot13a.c >$(BUILD_DIR)/xlate

$(BUILD_DIR)/rot13c2.c: rot13c2.c.in $(LIBAPUE) $(BUILD_DIR)/xlate | $(BUILD_DIR)
	sed '/same/q' rot13c2.c.in >$(BUILD_DIR)/rot13c2.c
	cat $(BUILD_DIR)/xlate >>$(BUILD_DIR)/rot13c2.c
	sed '1,/same/d' rot13c2.c.in >>$(BUILD_DIR)/rot13c2.c

$(BUILD_DIR)/rot13c2: $(BUILD_DIR)/rot13c2.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/lockfile.o: lockfile.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc