# 指定CMake最低版本要求
cmake_minimum_required(VERSION 3.10)

# 定义项目名称和使用的语言
project(apue C)

# 设置C标准为C99（对应你的Makefile中的 -std=c99）
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# 定义根目录变量（类似于Makefile中的ROOT）
set(ROOT ${CMAKE_SOURCE_DIR})

# 全局编译定义（对应Makefile中的CFLAGS）
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -m64 -Wall -DMACOS -D_DARWIN_C_SOURCE")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DNAME_MAX=_XOPEN_NAME_MAX")

# 全局包含目录（对应Makefile中的 -I$(ROOT)/include）
include_directories(${ROOT}/include)

# 添加子目录
add_subdirectory(lib)
add_subdirectory(intro)