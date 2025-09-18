ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

PROGS = doatexit echoarg getrlimit hello1 testjmp

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/opendata.o $(BUILD_DIR)/scope.o

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/opendata.o: opendata.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

$(BUILD_DIR)/scope.o: scope.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
