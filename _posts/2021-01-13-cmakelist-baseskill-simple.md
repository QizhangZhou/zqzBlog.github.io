---
title: CMakeLists编写基础范例备查
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: CMakeLists编写基础范例备查
tags:
- cmakeList
- tech
---

### CMAKE基础框架

```cmake
#cmake verson，指定cmake版本 
cmake_minimum_required(VERSION 3.14.0)


#设置语言，两种方式
add_definitions(-std=c++11)
#set(CMAKE_CXX_STANDARD 11)


#设置环境变量
add_definitions( -DGPU -DCUDNN )


#project name，指定项目的名称
set(PROJECT_NAME SOME_BASE)
project(${PROJECT_NAME})


#head file path，头文件目录
#include_directories()


#source directory，源文件目录
aux_source_directory(src .)


#add executable file，添加要编译的可执行文件
set(DIR_SRCS main.cpp)
add_executable(${PROJECT_NAME} ${DIR_SRCS})


#add link library，添加可执行文件所需要的库，就添加该库的名称
#target_link_libraries(${PROJECT_NAME} name)


#build so
#STATIC库是目标文件的归档文件（静态链接库），在链接其它目标的时候使用。
#SHARED库会被动态链接（动态链接库），在运行时会被加载
#MODULE库是一种不会被链接到其它目标中的插件
#add_library(${PROJECT_NAME} SHARED ${SRC})
```

### 编写Shell
使得缓存文件放在build目录下，并在cmake后删除build文件
```shell
#!/bin/bash

#set project name
project_name="someBase"

# make direction for build
mkdir build

# get work path
build_path=$(dirname $0)

# Build files have been written to build/
cd build
cmake ${build_path}/../

# make and copy binary file
make
cp ${project_name} ../
cd .. 

rm -r build/
echo "#####################################"
./${project_name}
```
