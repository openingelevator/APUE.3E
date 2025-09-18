ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

PROGS = fileflags hole mycat seek

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/setfl.o

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/setfl.o: setfl.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/* file.hole

include $(ROOT)/Make.libapue.inc
