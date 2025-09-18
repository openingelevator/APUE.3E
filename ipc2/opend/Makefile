ROOT=../..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lsocket -lnsl
endif

PROGS = opend.poll opend.select

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,opend.poll opend.select)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/opend.poll: $(BUILD_DIR)/main.o $(BUILD_DIR)/request.o $(BUILD_DIR)/cliargs.o $(BUILD_DIR)/client.o $(BUILD_DIR)/loop.poll.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/main.o $(BUILD_DIR)/cliargs.o $(BUILD_DIR)/client.o $(BUILD_DIR)/request.o $(BUILD_DIR)/loop.poll.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/opend.select: $(BUILD_DIR)/main.o $(BUILD_DIR)/request.o $(BUILD_DIR)/cliargs.o $(BUILD_DIR)/client.o $(BUILD_DIR)/loop.select.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/main.o $(BUILD_DIR)/cliargs.o $(BUILD_DIR)/client.o $(BUILD_DIR)/request.o $(BUILD_DIR)/loop.select.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/main.o: main.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c main.c -o $@

$(BUILD_DIR)/cliargs.o: cliargs.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c cliargs.c -o $@

$(BUILD_DIR)/request.o: request.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c request.c -o $@

$(BUILD_DIR)/client.o: client.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c client.c -o $@

$(BUILD_DIR)/loop.poll.o: loop.poll.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c loop.poll.c -o $@

$(BUILD_DIR)/loop.select.o: loop.select.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c loop.select.c -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
