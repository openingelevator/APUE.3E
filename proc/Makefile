ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ACCT=
ACCTFLAGS=
ifeq "$(PLATFORM)" "linux"
  ACCT=pracct
  ACCTFLAGS = -DHAS_AXSIG -DHAS_ACORE
endif
ifeq "$(PLATFORM)" "macos"
  ACCT=pracct
  ACCTFLAGS = -DHAS_AXSIG -DHAS_ACORE
endif
ifeq "$(PLATFORM)" "solaris"
  ACCT=pracct
  ACCTFLAGS = -DHAS_AC_STAT
endif

PROGS = echoall exec1 exec2 fork1 fork2 nice pruids tellwait1 tellwait2 test1 times1 vfork1 wait1
MOREPROGS = systest1 systest3

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS) $(MOREPROGS)) $(BUILD_DIR)/system.o $(BUILD_DIR)/$(ACCT)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/systest1: system.o systest1.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ systest1.o system.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/systest3: system.o systest3.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ systest3.o system.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/pracct: pracct.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $(ACCTFLAGS) -o $@ pracct.c $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/system.o: system.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
