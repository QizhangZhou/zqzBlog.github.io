---
title: Linux下安装Python3.8
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: Linux下安装Python3.8
tags:
- linux
- python
- tech
---


以下是安装脚本

```shell
sudo mkdir py3
cd py3
sudo wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz
tar -xvzf Python-3.8.1.tgz
cd Python-3.8.1
sudo mkdir -p /usr/local/python3
./configure --prefix=/usr/local/python3
make
sudo make install

rm -rf /usr/bin/python3
ln -s /usr/local/python3/bin/python3.8 /usr/bin/python3
sudo rm /usr/bin/lsb_release

ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3

```
