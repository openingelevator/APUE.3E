# 查找lib目录下所有的C源文件
file(GLOB LIB_SOURCES "*.c")

# 添加必要的预处理器定义，但移除与apue.h中重复的_XOPEN_SOURCE
add_definitions(
    -D_DARWIN_C_SOURCE
    -DMACOS  # 添加MACOS定义，确保包含ioctl.h
)

# 创建静态库（对应Makefile中的libapue.a）
add_library(apue STATIC ${LIB_SOURCES})

# 设置库的属性
set_target_properties(apue PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY ${ROOT}/lib
 )
