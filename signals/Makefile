ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

CLD =

ifeq "$(PLATFORM)" "linux"
  CLD = child
endif
ifeq "$(PLATFORM)" "solaris"
  CLD = child
endif

PROGS = critical mask read1 read2 reenter sigtstp sigusr suspend1 suspend2
MOREPROGS = systest2 tsleep2

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS) $(MOREPROGS)) $(BUILD_DIR)/abort.o $(BUILD_DIR)/sleep1.o $(BUILD_DIR)/sleep2.o $(BUILD_DIR)/system.o $(BUILD_DIR)/$(CLD)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/tsleep2: tsleep2.o sleep2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ tsleep2.o sleep2.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/systest2: systest2.o system.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ systest2.o system.o $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/%.o: %.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/* file.hole $(CLD)

include $(ROOT)/Make.libapue.inc
