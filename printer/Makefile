ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

PROGS = print printd
HDRS = print.h ipp.h

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/util.o: util.c $(HDRS) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c util.c -o $@

$(BUILD_DIR)/print.o: print.c $(HDRS) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c print.c -o $@

$(BUILD_DIR)/printd.o: printd.c $(HDRS) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c printd.c -o $@

$(BUILD_DIR)/print: $(BUILD_DIR)/print.o $(BUILD_DIR)/util.o $(ROOT)/sockets/clconn2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/print.o $(BUILD_DIR)/util.o $(ROOT)/sockets/clconn2.o $(LDFLAGS) $(LDDIR) $(LDLIBS)

$(BUILD_DIR)/printd: $(BUILD_DIR)/printd.o $(BUILD_DIR)/util.o $(ROOT)/sockets/clconn2.o $(ROOT)/sockets/initsrv2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/printd.o $(BUILD_DIR)/util.o $(ROOT)/sockets/clconn2.o $(ROOT)/sockets/initsrv2.o \
		$(LDFLAGS) $(LDDIR) $(LDLIBS)

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
