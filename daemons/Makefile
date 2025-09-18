ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,init reread reread2 single)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: $(BUILD_DIR)/%.o | $(BUILD_DIR)
	cp $< $@

$(BUILD_DIR)/%.o: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
