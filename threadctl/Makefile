ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

TOUT =
ifeq "$(PLATFORM)" "freebsd"
  EXTRALIBS = -pthread
endif
ifeq "$(PLATFORM)" "linux"
  EXTRALIBS = -pthread
  TOUT = timeout.o
endif
ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS = -lpthread
  TOUT = timeout.o
endif

PROGS = atfork suspend

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS)) $(BUILD_DIR)/detach.o $(BUILD_DIR)/getenv1.o $(BUILD_DIR)/getenv2.o $(BUILD_DIR)/getenv3.o $(BUILD_DIR)/$(TOUT)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%.o: %.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc
