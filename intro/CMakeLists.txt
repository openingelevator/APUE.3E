# 查找intro目录下所有的C源文件
file(GLOB INTRO_SOURCES "*.c")

# 为每个源文件创建可执行文件
foreach(SOURCE_FILE ${INTRO_SOURCES})
    # 获取文件名（不含扩展名）作为可执行文件名
    get_filename_component(EXECUTABLE_NAME ${SOURCE_FILE} NAME_WE)
    
    # 添加可执行文件目标
    add_executable(${EXECUTABLE_NAME} ${SOURCE_FILE})
    
    # 链接apue库
    target_link_libraries(${EXECUTABLE_NAME} apue)
    
    # 设置输出目录
    set_target_properties(${EXECUTABLE_NAME} PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    )
endforeach()