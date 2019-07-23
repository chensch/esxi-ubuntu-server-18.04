# 在Esxi6.5上安装ubuntu-server-18.04

## #通过Esxi的WEB UI上传ubuntu-server-18.04镜像

## #新建虚拟机，内存2048，CPU 2，磁盘20GB

## #安装阶段网络配置

> 在10.10.105.103上的机子安装Ubuntu的网络ip依次为：10.10.105.105，10.10.105.107，10.10.105.109...
- Network connections > 选择ubuntu的网卡（这里是ens160）> Edit IPv4
- IPv4 Method: Manual
- Subnet: 10.10.105.0/24
- Address: 10.10.105.105(每台分配不同的ip)
- Gateway: 10.10.105.254
- Save

## #文件系统
> 简化安装，不手动分区

- Filesystem setup > Use An Entire Disk

## #系统安装好
- 移除安装盘>重启
