# [Linux]openSUSE 为服务器 ssh connection refused

两种原因：
1. suse 上sshd服务没开
2. suse 上防火墙把所有 IP 对22端口的访问都禁止了

解决
1. 启动 sshd 服务
2. 配置防火墙打开 22 端口

## sshd

```bash
# 开启sshd
sudo /usr/sbin/rcsshd restart sshd
# 开机自动启动ssh命令
sudo systemctl enable ssh
# 关闭ssh开机自动启动命令
sudo systemctl disable ssh
# 单次开启ssh
sudo systemctl start ssh
# 单次关闭ssh
sudo systemctl stop ssh
# 设置好后重启系统
reboot
#查看ssh是否启动，看到Active: active (running)即表示成功
sudo systemctl status ssh
```

## firewalld

1. firewalld的基本使用

```bash
**启动**： systemctl start firewalld
**关闭**： systemctl stop firewalld
**查看状态**： systemctl status firewalld 
**开机禁用**： systemctl disable firewalld
**开机启用**： systemctl enable firewalld
屏蔽:systemctl mask firewalld 屏蔽防火墙服务（让它不能启动） ln -s '/dev/null''/etc/systemd/system/firewalld.service' 
取消屏蔽:systemctl unmask firewalld 显示服务（如 firewalld.service） rm '/etc/systemd/system/firewalld.service'
``` 
2. systemctl是服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。

```bash
启动一个服务：systemctl start firewalld.service
关闭一个服务：systemctl stop firewalld.service
重启一个服务：systemctl restart firewalld.service
显示一个服务的状态：systemctl status firewalld.service
在开机时启用一个服务：systemctl enable firewalld.service
在开机时禁用一个服务：systemctl disable firewalld.service
查看服务是否开机启动：systemctl is-enabled firewalld.service
查看已启动的服务列表：systemctl list-unit-files|grep enabled
查看启动失败的服务列表：systemctl --failed
```

3. 配置firewalld-cmd

```bash
查看版本： firewall-cmd --version
查看帮助： firewall-cmd --help
显示状态： firewall-cmd --state
查看所有打开的端口： firewall-cmd --zone=public --list-ports
更新防火墙规则： firewall-cmd --reload
查看区域信息:  firewall-cmd --get-active-zones
列出全部启用的区域的特性：firewall-cmd --list-all-zones
获取默认区域的网络设置：firewall-cmd --get-default-zone
查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0
拒绝所有包：firewall-cmd --panic-on
取消拒绝状态： firewall-cmd --panic-off
查看是否拒绝： firewall-cmd --query-panic
获取所有支持的服务：firewall-cmd --get-services
调整默认策略（默认拒绝所有访问，改成允许所有访问）：
firewall-cmd --permanent --zone=public --set-target=ACCEPT
firewall-cmd --reload
对某个IP开放多个端口：firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="10.159.60.29" port protocol="tcp" port="1:65535" accept"
firewall-cmd --reload
获取所有支持的ICMP类型：firewall-cmd --get-icmptypes

```

4. 开启与删除一个端口

```bash
添加
firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
重新载入
firewall-cmd --reload
查看
firewall-cmd --zone= public --query-port=80/tcp
删除
firewall-cmd --zone= public --remove-port=80/tcp --permanent
```

5. iptables

```bash
但是即使服务运行了,防火墙也不一定起作用,你还得看防火墙规则的设置: iptables -L

在此说一下关于启动和关闭防火墙的命令:

1) 重启后生效

开启：chkconfig iptables on

关闭：chkconfig iptables off

2) 即时生效，重启后失效

开启：service iptables start

关闭：service iptables stop
```
