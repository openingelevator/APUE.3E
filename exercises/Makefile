ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "freebsd"
  GETPW = getpw44bsd
  FMEM = fmemopen.o
  EXTRALIBS=-pthread
endif
ifeq "$(PLATFORM)" "linux"
  GETPW = getpwsvr4
  FMEM =
  EXTRALIBS=-pthread
endif
ifeq "$(PLATFORM)" "macos"
  GETPW = getpw44bsd
  FMEM = fmemopen.o
endif
ifeq "$(PLATFORM)" "solaris"
  GETPW = getpwsvr4
  FMEM =
endif

PROGS =	bo fifo1 getlogin goodexit longpath pendlock prtime sizepipe vfork3 zombie

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/asyncsocket.o $(BUILD_DIR)/openmax.o $(BUILD_DIR)/sleep.o $(BUILD_DIR)/sleepus_poll.o $(BUILD_DIR)/sleepus_select.o $(BUILD_DIR)/$(GETPW) $(BUILD_DIR)/$(FMEM)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%.o: %.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
