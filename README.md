# cmake

## #0 demo

```
cmake_minimum_required(VERSION 3.5.1)
project(typhoon VERSION 1.2.3)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(TARGET_NAME ${PROJECT_NAME})

find_package(PkgConfig REQUIRED)
find_package(Boost REQUIRED COMPONENTS system thread)

include_directories(
  ${Boost_INCLUDE_DIRS}
)

link_directories (
  ${Boost_LIBRARY_DIRS}
)

add_library(${TARGET_NAME} SHARED
  src/node.cc
)

target_link_libraries(${TARGET_NAME}
  ${Boost_LIBRARIES}
)

add_executable(${TARGET_NAME}_runner main.cc)

target_link_libraries(${TARGET_NAME}_runner
    ${TARGET_NAME}
)
```

## #1 内置变量

### #1.1 获取值

- ­CMAKE_MAJOR_VERSION: cmake 主版本号，比如 3.4.1 中的 3
- CMAKE_MINOR_VERSION: cmake 主版本号，比如 3.4.1 中的 4
- CMAKE_PATCH_VERSION: cmake 主版本号，比如 3.4.1 中的 1
- CMAKE_SYSTEM: 系统名称，比如 Linux-­2.6.22
- CMAKE_SYSTEM_NAME: '不包含版本的系统名'，比如 Linux
- ­CMAKE_SYSTEM_VERSION：'系统(内核)版本'，比如 2.6.22
- ­CMAKE_SYSTEM_PROCESSOR：'处理器名称',比如 i686
- PROJECT_SOURCE_DIR: 工程文件夹路径
- PROJECT_BINARY_DIR: 运行cmake路径

### #1.2 设置值

- CMAKE_CXX_STANDARD

设置C++标准

```
set(CMAKE_CXX_STANDARD 14)
```

- CMAKE_BUILD_TYPE

设置单个配置生成器上的编译类型

```
# set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_BUILD_TYPE "Release")
```

- BUILD_SHARED_LIBS

是否生成动态库

```
# set(BUILD_SHARED_LIBS ON)
set(BUILD_SHARED_LIBS OFF)
```

- CMAKE_*_OUTPUT_DIRECTORY

设置输出目录

```
# 全局设置
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# 单个目标
set_target_properties( targets...
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)
```


## #2 base

### #2.1 project

> 项目名

```txt
project(typhoon VERSION 1.2.3)
```

> 隐藏变量

- ${PROJECT_NAME}: "typhoon"
- ${PROJECT_VERSION}: 1.2.3
- ${PROJECT_VERSION_MAJOR}: 1
- ${PROJECT_VERSION_MINOR}: 2
- ${PROJECT_VERSION_PATCH}: 3


### #2.2 find_package

CMake 会到变量CMAKE_MODULE_PATH 指示的目录下查找文件 Findname.cmake 并执行


```
find_package(Boost REQUIRED COMPONENTS system thread)
```

> 隐藏变量

- <NAME>_FOUND: 是否找到
- <NAME>_INCLUDE_DIRS or <NAME>_INCLUDES
- <NAME>_LIBRARIES or <NAME>_LIBRARIES or <NAME>_LIBS
- <NAME>_DEFINITIONS


### #2.3 pkg_check_modules

### #2.4 pkg_search_module

### #2.5 include_directories

### #2.6 link_directories

### #2.7 target_link_libraries

### #2.8 add_executable
