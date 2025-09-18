ROOT=../..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lsocket -lnsl
endif

PROGS = opend

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/opend: $(BUILD_DIR)/main.o $(BUILD_DIR)/request.o $(BUILD_DIR)/cliargs.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/main.o $(BUILD_DIR)/cliargs.o $(BUILD_DIR)/request.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/main.o: main.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c main.c -o $@

$(BUILD_DIR)/cliargs.o: cliargs.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c cliargs.c -o $@

$(BUILD_DIR)/request.o: request.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c request.c -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
