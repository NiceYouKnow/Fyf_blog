# 简介
一些使用Ubuntu过程中积累的小技巧。

## ubuntu（desktop）使用vi编辑器时输入异常且按方向键乱码

* 卸载

    sudo apt-get remove vim-common

* 安装

    sudo apt-get install vim

## 开启root登录ssh的方式（实践版本为20.04）

* 设置root密码

    sudo passwd root

* 修改ssh配置

    sudo vim /etc/ssh/sshd_config

```
PermitRootLogin without-password
修改为
PermitRootLogin yes
```

* 重启sshd服务

    sudo systemctl restart sshd

## 修改IP地址

ubuntu18以后的IP配置文件一般存放在/etc/netplan/****.yaml文件中，所以修改IP相关信息得修改该文件。

* sudo vi /etc/netplan/****.yaml

文件示例：
```
network:
  ethernets:
    ens233:     #配置的网卡的名称
      addresses: [192.168.2.2/24]    #配置的静态ip地址和掩码
      dhcp4: no    #关闭DHCP，需要打开DHCP则写yes
      optional: true
      gateway4: 192.168.2.254    #网关地址
      nameservers:
         addresses: [192.168.31.1,114.114.114.114]    #DNS服务器地址，多个DNS服务器地址需要用英文逗号分隔开
  version: 2
  renderer: networkd    #指定后端采用systemd-networkd或者Network Manager，可不填写则默认使用systemd-workd
```

* 重新应用yaml配置文件

    sudo netplan apply
