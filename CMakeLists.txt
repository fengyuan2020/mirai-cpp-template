# 项目名称
project(my-qqrobot)
# 设置项目的 C++ 标准
set(CMAKE_CXX_STANDARD 11)

# 不要构建 mirai-cpp 自带的 examples
set(MIRAI_CPP_BUILD_EXAMPLES OFF)
# 添加子模块 mirai-cpp
add_subdirectory(mirai-cpp)

# 源码以 UTF-8 编码保存，使用 MSVC 编译器时需要加编译参数提供支持
if(MSVC)
    add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
    add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")
    message(STATUS "optional: /UTF-8")   
endif(MSVC)

add_executable(${PROJECT_NAME} src/main.cpp)
# 设置头文件目录
include_directories(include)
# 链接 mirai-cpp
target_link_libraries(${PROJECT_NAME} PRIVATE mirai-cpp)
# 使用 mirai-cpp 静态库
target_compile_definitions(${PROJECT_NAME} PRIVATE MIRAICPP_STATICLIB)