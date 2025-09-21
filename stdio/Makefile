ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "linux"
  MEMSTR = memstr
else
  MEMSTR =
endif

PROGS = buf fgetsfputs getcharbug getcputc mkstemp tempfiles

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(addprefix $(BUILD_DIR)/,$(MEMSTR))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

clean:
	rm -f $(BUILD_DIR)/* $(MEMSTR)

include $(ROOT)/Make.libapue.inc
