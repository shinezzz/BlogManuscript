# ubuntu终端设置代理ss/ssr

## ss

1. 利用proxychains在终端使用socks5代理

    ```bash
    git clone https://github.com/rofl0r/proxychains-ng.git
    cd proxychains-ng
    ./configure
    make && make install
    cp ./src/proxychains.conf /etc/proxychains.conf
    cd .. && rm -rf proxychains-ng
    vim /etc/proxychains.conf
    ```

    将socks4 127.0.0.1 9095改为socks5 127.0.0.1 1080

2. export的方法

    - http协议

    ```bash
    export http_proxy=http://127.0.0.1:1080
    export https_proxy=http://127.0.0.1:1080
    ## 关闭
    unset http_proxy;
    unset https_proxy
    ```

    - sock5协议

    ```bash
    export http_proxy="socks5://127.0.0.1:1080"
    export https_proxy="socks5://127.0.0.1:1080"
    # export ALL_PROXY=socks5://127.0.0.1:1080
    ```

    - 设置alias

    ```bash
     alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
     alias unsetproxy="unset ALL_PROXY"
    ```

## ssr

SSR,并且走的http的代理端口是12333

```bash
export http_proxy=http://127.0.0.1:12333
export https_proxy=http://127.0.0.1:12333
```

- [ ] 用socks5理论上也可以，但是我一直出问题。

## ss/ssr加速git

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

## 改相应工具的配置，比如apt的配置

```bash
sudo vim /etc/apt/apt.conf
```

在文件末尾加入下面这行

```bash
Acquire::http::Proxy "http://proxyAddress:port"
```
