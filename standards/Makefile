ROOT=..
PLATFORM=$(shell $(ROOT)/systype.sh)
include $(ROOT)/Make.defines.$(PLATFORM)

BUILD_DIR=build

PROGS = conf options

all: $(BUILD_DIR) $(addprefix $(BUILD_DIR)/,$(PROGS))

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# 可执行程序输出到 build 目录
$(BUILD_DIR)/%: $(BUILD_DIR)/%.c $(LIBAPUE) | $(BUILD_DIR)
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS) $(LDLIBS)

# conf.c 生成到 build 目录
$(BUILD_DIR)/conf.c: makeconf.awk $(BUILD_DIR)/sysconf.sym $(BUILD_DIR)/pathconf.sym | $(BUILD_DIR)
	$(AWK) -f makeconf.awk >$@

# sysconf.sym 生成到 build 目录
$(BUILD_DIR)/sysconf.sym: sysconf-lim.sym | $(BUILD_DIR)
	grep -v "^#" $< >$@

# pathconf.sym 生成到 build 目录
$(BUILD_DIR)/pathconf.sym: pathconf-lim.sym | $(BUILD_DIR)
	grep -v "^#" $< >$@

# options.c 生成到 build 目录
$(BUILD_DIR)/options.c: makeopt.awk $(BUILD_DIR)/sysopt.sym $(BUILD_DIR)/pathopt.sym | $(BUILD_DIR)
	$(AWK) -f makeopt.awk >$@

# sysopt.sym 生成到 build 目录
$(BUILD_DIR)/sysopt.sym: sysconf-opt.sym | $(BUILD_DIR)
	grep -v "^#" $< >$@

# pathopt.sym 生成到 build 目录
$(BUILD_DIR)/pathopt.sym: pathconf-opt.sym | $(BUILD_DIR)
	grep -v "^#" $< >$@

clean:
	rm -rf $(BUILD_DIR)/*

include $(ROOT)/Make.libapue.inc