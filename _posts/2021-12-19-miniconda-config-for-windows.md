---
title: miniconda配置 for Windows
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: miniconda配置 for Windows
tags:
- miniconda
- tech
---


## Windows配置

1、安装好conda之后，生成在C:\Users\Administrator目录下生成.condarc文件
```
conda config --set show_channel_urls yes
```
2、删除原来的内容，填入以下内容，设置镜像
```
channels:
  - defaults
show_channel_urls: true
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

```

3、创建python环境
```
conda activate python_3.6
```

4、激活python环境
```
conda create -n python_3.6 python=3.6
```

5、退出环境
```
conda deactivate
```

6、利用conda install命令安装所需工具,例如pandas
```
conda install pandas
```
7、看所有工具包
```
conda list
```


#### Windows PowerShell 无法激活环境解决方法
```
conda init powershell
```