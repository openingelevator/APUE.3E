ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS=-lsocket -lnsl
endif

PROGS = pty

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(BUILD_DIR)/pty: main.o loop.o driver.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ main.o loop.o driver.o $(LDFLAGS) $(LDLIBS)

main.o: main.c $(LIBAPUE)
	$(CC) $(CFLAGS) -c main.c -o main.o

loop.o: loop.c $(LIBAPUE)
	$(CC) $(CFLAGS) -c loop.c -o loop.o

driver.o: driver.c $(LIBAPUE)
	$(CC) $(CFLAGS) -c driver.c -o driver.o

clean:
	rm -f $(BUILD_DIR)/* *.o

include $(ROOT)/Make.libapue.inc
