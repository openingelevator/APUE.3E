ROOT=..
EXTRALIBS=-pthread
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

BAR =
ifeq "$(PLATFORM)" "macos"
  TLOCK =
  EXTRALIBS=-pthread
else
  TLOCK = timedlock
endif
ifeq "$(PLATFORM)" "linux"
  BAR = barrier
  EXTRALIBS=-pthread -lrt -lbsd
endif
ifeq "$(PLATFORM)" "freebsd"
  BAR = barrier
  EXTRALIBS=-pthread
endif
ifeq "$(PLATFORM)" "solaris"
  BAR = barrier
  EXTRALIBS=-lpthread -lrt
endif

PROGS = badexit2 cleanup exitstatus threadid
OBJS =
ifneq "$(TLOCK)" ""
OBJS += $(BUILD_DIR)/$(TLOCK)
endif
ifneq "$(BAR)" ""
OBJS += $(BUILD_DIR)/$(BAR)
endif

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/condvar.o $(BUILD_DIR)/maketimeout.o $(BUILD_DIR)/mutex1.o $(BUILD_DIR)/mutex2.o $(BUILD_DIR)/mutex3.o $(BUILD_DIR)/rwlock.o $(OBJS)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%.o: %.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
