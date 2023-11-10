---
title: SpringBoot Maven下载依赖设置方式
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: SrpingBoot在增加包依赖的时候，由于服务器问题，下载相关依赖会很慢，这里提供一种aliyun的代理设置方式。
tags:
- KV
- database
- tech
---
### SpringBoot Maven下载依赖设置方式

idea为例子：  
右键点击project -> 选择maven ->选择open setting.xml  
增加以下设置

```xml

    <mirrors>
        <mirror>
            <id>aliyunmaven</id>
            <mirrorOf>central</mirrorOf>
            <name>阿里云公共仓库</name>
            <url>https://maven.aliyun.com/repository/central</url>
        </mirror>
        <mirror>
            <id>repo1</id>
            <mirrorOf>central</mirrorOf>
            <name>central repo</name>
            <url>http://repo1.maven.org/maven2/</url>
        </mirror>
        <mirror>
            <id>aliyunmaven</id>
            <mirrorOf>apache snapshots</mirrorOf>
            <name>阿里云阿帕奇仓库</name>
            <url>https://maven.aliyun.com/repository/apache-snapshots</url>
        </mirror>
    </mirrors>
    <proxies/>
    <activeProfiles/>
    <profiles>
        <profile>
            <repositories>
                <repository>
                    <id>aliyunmaven</id>
                    <name>aliyunmaven</name>
                    <url>https://maven.aliyun.com/repository/public</url>
                    <layout>default</layout>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
                <repository>
                    <id>MavenCentral</id>
                    <url>http://repo1.maven.org/maven2/</url>
                </repository>
                <repository>
                    <id>aliyunmavenApache</id>
                    <url>https://maven.aliyun.com/repository/apache-snapshots</url>
                </repository>
            </repositories>
        </profile>
    </profiles>
```