ROOT=../..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lsocket -lnsl
endif

PROGS = openclient

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/openclient: $(BUILD_DIR)/main.o $(BUILD_DIR)/open.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(BUILD_DIR)/main.o $(BUILD_DIR)/open.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/main.o: main.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c main.c -o $@

$(BUILD_DIR)/open.o: open.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c open.c -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
