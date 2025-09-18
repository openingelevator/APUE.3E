ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

LIBMISC = $(BUILD_DIR)/libapue_db.a
COMM_OBJ = $(BUILD_DIR)/db.o

ifeq "$(PLATFORM)" "solaris"
  LDCMD=$(LD) -64 -G -Bdynamic -R/lib/64:/usr/ucblib/sparcv9 -o $(BUILD_DIR)/libapue_db.so.1 -L/lib/64 -L/usr/ucblib/sparcv9 -L$(ROOT)/lib -lapue $(BUILD_DIR)/db.o
  EXTRALD=-m64 -R.
else
  LDCMD=$(CC) -shared -Wl,-dylib -o $(BUILD_DIR)/libapue_db.so.1 -L$(ROOT)/lib -lapue -lc $(BUILD_DIR)/db.o
endif
ifeq "$(PLATFORM)" "linux"
  EXTRALD=-Wl,-rpath=.
endif
ifeq "$(PLATFORM)" "freebsd"
  EXTRALD=-Wl,-rpath=.
endif
ifeq "$(PLATFORM)" "macos"
  EXTRALD=-R.
endif

all: $(BUILD_DIR) $(BUILD_DIR)/libapue_db.so.1 $(BUILD_DIR)/t4 $(LIBMISC)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(LIBMISC): $(COMM_OBJ) $(LIBAPUE)
	$(AR) rsv $@ $(COMM_OBJ)
	$(RANLIB) $@

$(BUILD_DIR)/libapue_db.so.1: db.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) -fPIC $(CFLAGS) -c db.c -o $(BUILD_DIR)/db.o
	$(LDCMD)
	ln -sf libapue_db.so.1 $(BUILD_DIR)/libapue_db.so

$(BUILD_DIR)/t4: t4.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c -I. t4.c -o $(BUILD_DIR)/t4.o
	$(CC) $(EXTRALD) -o $@ $(BUILD_DIR)/t4.o -L$(ROOT)/lib -L$(BUILD_DIR) -lapue_db -lapue

$(BUILD_DIR)/db.o: db.c | $(BUILD_DIR)
	$(CC) -fPIC $(CFLAGS) -c db.c -o $@

clean:
	rm -f $(BUILD_DIR)/* *.dat *.idx

include $(ROOT)/Make.libapue.inc
