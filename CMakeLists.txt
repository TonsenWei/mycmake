cmake_minimum_required(VERSION 3.0)
PROJECT(MYSWAP)

# -g参数会生成调试信息，比如在main中增加了断点，使用-g时会在编译时加入这个断点信息
set(CMAKE_CXX_FLAGS "-g")

# 生成一个静态库，会生成一个libswap.a文件
# add_library(swap "${CMAKE_CURRENT_SOURCE_DIR}/src/src/swap.cpp")
# 生成一个共享库，会生成一个libswap_shared.dll文件
# add_library(swap_shared SHARED "${CMAKE_CURRENT_SOURCE_DIR}/src/src/swap.cpp")

# 头文件目录
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/src/include")
# 查找库的目录
link_directories("${CMAKE_CURRENT_SOURCE_DIR}/libs")
# 源文件目录，使用了库，不再需要swap.cpp这个源文件
# AUX_SOURCE_DIRECTORY("${CMAKE_CURRENT_SOURCE_DIR}/src/src" DIR_SRCS)

# 生成可执行文件，这里没有写swap.cpp,是因为swap.cpp和swap.h编译成了链接库，
# 后面再使用target_link_libraries把库链接到my_cmake_swap
# add_executable(my_cmake_swap main.cpp ${DIR_SRCS})
add_executable(my_cmake_swap main.cpp)

# 把可执行程序链接到共享库（动态链接库）
# target_link_libraries(my_cmake_swap swap_shared)
# 也可以使用下面的，把可执行程序链接到静态库
# target_link_libraries(my_cmake_swap libswap_shared.dll)
# 使用静态链接库，编译链接后，就包含在可执行文件中了，不需要再拷贝到与可执行文件相同目录下
target_link_libraries(my_cmake_swap libswap.a)