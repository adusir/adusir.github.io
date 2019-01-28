---
title: ESXi6.7官方镜像封装网卡驱动
description: 
categories:
 - 环境搭建
tags:
 - ESXi
 - 网卡驱动
---

# ESXi6.7官方镜像封装网卡驱动

今天心血来潮，想在空闲的台式机上安装ESXi6.7，以便同时使用windows和linux，充分利用机器的性能；但在安装过程中出现了一个小问题，就是ESXi不支持我的网卡，再网上一搜索，发现都有这样的问题，但没有找到封装好网卡的镜像，于是，就开始动手自己解决，顺便记录用以备忘。

步骤为：
1. 安装VMware PowerCLI
2. 下载ESXi-Customizer-PS,下载ESXi6.7，下载网卡驱动
3. 使用ESXi-Customizer-PS把网卡驱动封装进镜像
4. 最后使用rufus制作启动U盘


## 如何安装VMware PowerCLI

由于我是win10比较新，版本为5.1，直接通过Install-Module安装

``` shell
Install-Module -Name VMware.PowerCLI
```

VMware.PowerCLI安装官方指导见[https://www.powershellgallery.com/packages/VMware.PowerCLI/11.1.0.11289667](https://www.powershellgallery.com/packages/VMware.PowerCLI/11.1.0.11289667)

## ESXi-Customizer-PS 

用于封装自定义镜像的工具非vmware官方提供，是第三方，地址为：[https://www.v-front.de/p/esxi-customizer-ps.html](https://www.v-front.de/p/esxi-customizer-ps.html)
，里面也有说明怎么使用。


## ESXi6.7&&网卡驱动
1. ESXi现在的名称叫hypervisor，下载地址见[https://my.vmware.com/cn/web/vmware/evalcenter?p=free-esxi6](https://my.vmware.com/cn/web/vmware/evalcenter?p=free-esxi6)，对我们这种使用场景来说是完全免费的(不需要管理一堆的机器).

2. 网卡驱动，需要先判断是否支持自己的网卡，网址为：[https://vibsdepot.v-front.de/wiki/index.php/List_of_currently_available_ESXi_packages](https://vibsdepot.v-front.de/wiki/index.php/List_of_currently_available_ESXi_packages)

3. 把powershell的安全策略中关于检查安装来源关闭
    ``` shell
    Set-ExecutionPolicy Unrestricted
    ```
4. 打包镜像
    ``` shell
    .\ESXi-Customizer-PS-v2.6.0.ps1 -v67 -vft -load net55-r8168
    ```
    
## 制作启动U盘

1. 下载 rufus,地址：[https://github.com/pbatard/rufus/releases/download/v3.4/rufus-3.4p.exe](https://github.com/pbatard/rufus/releases/download/v3.4/rufus-3.4p.exe)

2. 运行rufus，制作启动u盘


