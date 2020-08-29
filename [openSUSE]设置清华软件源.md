# openSUSE

## 手动设置

1. 禁用原有软件源

```bash
sudo zypper mr -da
```

2. 添加清华软件源

```bash
sudo zypper ar -fc https://mirrors.tuna.tsinghua.edu.cn/opensuse/distribution/leap/15.2/repo/oss TUNA:15.2:OSS
sudo zypper ar -fc https://mirrors.tuna.tsinghua.edu.cn/opensuse/distribution/leap/15.2/repo/non-oss TUNA:15.2:NON-OSS
sudo zypper ar -fc https://mirrors.tuna.tsinghua.edu.cn/opensuse/update/leap/15.2/oss TUNA:15.2:UPDATE-OSS
sudo zypper ar -fc https://mirrors.tuna.tsinghua.edu.cn/opensuse/update/leap/15.2/non-oss TUNA:15.2:UPDATE-NON-OSS
sudo zypper ar -fc https://mirrors.tuna.tsinghua.edu.cn/packman/suse/openSUSE_Leap_15.2/
```

3. 手动刷新软件源

```bash
sudo zypper ref
```
## 图形界面配置


1. 打开 YaST
2. 点击 Software 分组中的 Software Repositories
3. 将 download.opensuse.org 替换为相应的清华源的地址，把手动设置的几个源都改了
