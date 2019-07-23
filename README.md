# 在Esxi6.5上安装10台ubuntu-server-18.04

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

## #安装一台
- 移除安装盘>重启

---

## 使用刚装好那台ubuntu-server-18.04虚拟机创建模板

## #创建模板

- 关掉虚拟机电源
- 操作 > 导出（OVF模板） > 确定
- 等待文件下载到本地（应该有多个文件）

## #从模板创建ubuntu-server-18.04虚拟机

- 虚拟机 > 创建/注册虚拟机 > 从OVF或OVA文件部署虚拟机 
- 虚拟机名称自定义，单击“单击以选择或拖放文件”
- 选中所有创建模板下载的文件
- 等待上传完毕
- 用模板虚拟机的用户和密码登录

## #修改HOSTNAME

- sudo hostnamectl --static set-hostname [new-hostname](eg:sudo hostnamectl --static set-hostname pcl-2)
- exit后重新登陆

## #配置网络

- sudo vim /etc/netplan/50-cloud-init.yaml
- 进行以下配置，根据自己的网络情况适当改变（我配置10台，每个ip都要不一样）
  ```
   network:
       ethernets:
           ens160:
               dhcp: no
               addresses:
               - 10.10.105.105/24
               gateway4: 10.10.105.254
               nameservers:
                   addresses: [202.96.209.133, 8.8.8.8]
       version: 2
  ```
- 重新加载修改的配置文件`sudo netplan apply`
- ping baidu.com测试是否连通

-------------------

### 依据模板安装步骤依次安装其他虚拟机
