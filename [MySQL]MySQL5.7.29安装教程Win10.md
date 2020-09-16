# MySQL

## 1. 下载

官方网站：https://www.mysql.com/ 

选择DownLoads -> 点击 MySQL Community (GPL) Downloads -> 点击 MySQL Community Server -> 点击 Archives -> 选择 5.7.29 和 Microsoft Windows -> 下载 Windows (x86, 64-bit), ZIP Archive

## 2. 配置环境变量

此电脑 -> 属性 -> 高级系统设置 -> 环境变量 -> 系统变量

添加 MYSQL_HOME，就是那个压缩包的解压缩的地址：`C:\MySQL\mysql-5.7.29-winx64`

在 Path 中添加：`%MYSQL_HOME%\bin`

## 3. 配置my.ini文件

在 `C:\MySQL\mysql-5.7.29-winx64` 新建 `my.ini`，内容为：

```bash
[mysqld]
#端口号
port = 3306
#mysql-5.7.27-winx64的路径
basedir=C:\MySQL\mysql-5.7.29-winx64
#mysql-5.7.27-winx64的路径+\data
datadir=C:\MySQL\mysql-5.7.29-winx64\data 
#最大连接数
max_connections=200
#编码
character-set-server=utf8

default-storage-engine=INNODB

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

[mysql]
#编码
default-character-set=utf8 
```

## 4. 安装 MySQL

1. 在输入框内输入 cmd ，右键以**管理员的身份运行**
2. 在 cmd 中进入到 `C:\MySQL\mysql-5.7.29-winx64\bin`：输入 `mysqld -install`，应该返回**Service successfully installed**
3. 继续输入 `mysqld --initialize`，不会有提示
4. 再输入 `net start mysql`，MySQL 服务已经启动成功

## 5. 设置 MySQL 密码

1. 首先停止 MySQL 服务,输入命令行 `net stop mysql`
2. 打开文件 my.ini，在[mysqld]字段下任意一行添加 `skip-grant-tables`
3. 重启 MySQL,输入启动命令：`net start mysql`
4. 输入命令 `mysql -u root -p`，直接回车
5. 输入 `use mysql`
6. 输入 `update user set authentication_string=password("xxxxxx") where user="root";`，设置新密码，出现 OK，说明修改成功
7. 手动停止MySQL服务，在win10搜索栏内输入服务，找到MySQL。点击右键，然后点击停止即可。
8. 然后在刚刚的 my.ini 文件中删除 `skip-grant-tables` 这一行，保存关闭。
9. 再次启动cmd（管理员身份），输入启动命令 `net start mysql`，再输入 `mysql -u root -p`，再输入你刚刚设置的密码
10. 然后输入命令行use mysql验证一下，结果报错
11. 键入命令行alter user user() identified by "xxxxxx";我的密码是123456，因此我键入 alter user user() identified by "123456";回车！离胜利越来越近了！
12. 再次输入命令行use mysql验证一下，成功！

参考[博客](https://blog.csdn.net/weixin_43395911/article/details/99702121)