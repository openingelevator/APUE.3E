ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

ifeq "$(PLATFORM)" "solaris"
  EXTRALIBS = -lsocket -lnsl
endif

PROGS = ruptime ruptimed ruptimed-fd ruptimed-dg
MOREPROGS = findsvc ruptime-dg

# 所有目标文件路径指向 build 目录
OBJS = $(addprefix $(BUILD_DIR)/, ruptime.o clconn2.o ruptimed.o initsrv2.o ruptimed-fd.o ruptimed-dg.o)
TARGETS = $(addprefix $(BUILD_DIR)/, $(PROGS) $(MOREPROGS))

all: $(BUILD_DIR) $(TARGETS) $(BUILD_DIR)/clconn.o $(BUILD_DIR)/clconn2.o $(BUILD_DIR)/initsrv1.o $(BUILD_DIR)/initsrv2.o

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# 通用规则：生成可执行程序
$(BUILD_DIR)/%: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $< $(LDFLAGS) $(LDLIBS)

# 特殊规则：需要链接多个 .o 文件的目标
$(BUILD_DIR)/ruptime: $(BUILD_DIR)/ruptime.o $(BUILD_DIR)/clconn2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/ruptimed: $(BUILD_DIR)/ruptimed.o $(BUILD_DIR)/initsrv2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/ruptimed-fd: $(BUILD_DIR)/ruptimed-fd.o $(BUILD_DIR)/initsrv2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS) $(LDLIBS)

$(BUILD_DIR)/ruptimed-dg: $(BUILD_DIR)/ruptimed-dg.o $(BUILD_DIR)/initsrv2.o $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS) $(LDLIBS)

# 生成 .o 文件到 build 目录
$(BUILD_DIR)/%.o: %.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -rf $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc