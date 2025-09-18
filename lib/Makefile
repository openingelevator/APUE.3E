#
# Makefile for misc library.
#
ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

LIBMISC = $(BUILD_DIR)/libapue.a
OBJS   = bufargs.o cliconn.o clrfl.o \
			daemonize.o error.o errorlog.o lockreg.o locktest.o \
			openmax.o pathalloc.o popen.o prexit.o prmask.o \
			ptyfork.o ptyopen.o readn.o recvfd.o senderr.o sendfd.o \
			servaccept.o servlisten.o setfd.o setfl.o signal.o signalintr.o \
			sleepus.o spipe.o tellwait.o ttymodes.o writen.o

all: $(BUILD_DIR) $(LIBMISC) $(BUILD_DIR)/sleep.o

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(LIBMISC): $(OBJS)
	$(AR) rv $@ $?
	$(RANLIB) $@

$(BUILD_DIR)/sleep.o: sleep.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

%.o: %.c $(LIBAPUE)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(BUILD_DIR)/* *.o a.out core temp.* $(LIBMISC)

include $(ROOT)/Make.libapue.inc
