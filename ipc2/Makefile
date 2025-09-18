ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "freebsd"
  EXTRALIBS=-pthread
endif
ifeq "$(PLATFORM)" "linux"
  EXTRALIBS=-pthread
endif
ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lsocket -lnsl
endif

PROGS = bindunix pollmsg sendmsg
FDPASS =

ifeq "$(PLATFORM)" "linux"
	FDPASS = recvfd2.o sendfd2.o
endif
ifeq "$(PLATFORM)" "freebsd"
	FDPASS = recvfd2.o sendfd2.o
endif

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(addprefix $(BUILD_DIR)/,$(FDPASS))
	for i in open opend open.fe opend.fe; do \
		(cd $$i && $(MAKE) ) || exit 1; \
	done

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%.o: %.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*
	for i in open opend open.fe opend.fe; do \
		(cd $$i && $(MAKE) clean) || exit 1; \
	done

include $(ROOT)/Make.libapue.inc
