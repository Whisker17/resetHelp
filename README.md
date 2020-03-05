# 装机

1. 安装ss

```
sudo add-apt-repository ppa:hzwhuang/ss-qt5`
Ubuntu 18安装会失败: `仓库 “http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu bionic Release” 没有 Release 文件 的错误`
解决办法：
a. 编辑/etc/apt/sources.list.d/hzwhuang-ubuntu-ss-qt5-bionic.list 文件，将bionic (18.04版本代号)改成xenial（16.04版本代号）
b. 再执行 `sudo apt-get update`
c. 安装ss-qt5 `sudo apt-get install shadowsocks-qt5
```

```
安装完成后配置网络代理
a. 选择手动
b. http代理端口设置为 8118，其它不要管
c. Socks 主机设置为 127.0.0.1，端口设置为1080
```

```
google-chrome --proxy-server="socks5://127.0.0.1:1080"
然后安装SwitchyOmega，配置代理协议为 SOCKS5 ，代理服务器为 127.0.0.1 ，代理端口为 1080 。
```

2. 安装privoxy

```
sudo apt install privoxy
sudo vim /etc/privoxy/config
在最后加上
forward-socks5 / 127.0.0.1:1080 . 
listen-address 127.0.0.1:8118 （默认应该就是这个）
配置完重启服务
sudo /etc/init.d/privoxy restart
```

```
然后在 ~/.bashrc 中配置

#proxy default on
export http_proxy="127.0.0.1:8118"
export https_proxy="127.0.0.1:8118"

#proxy on and off
function proxy_off(){
    unset http_proxy
    unset https_proxy
    unset ftp_proxy
    unset rsync_proxy
    echo -e "已关闭代理"
}

function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
    export http_proxy="http://127.0.0.1:8118"
    export https_proxy=$http_proxy
    export ftp_proxy=$http_proxy
    export rsync_proxy=$http_proxy
    echo -e "已开启代理"
}

```

3. docker 的安装

   ```
   https://download.docker.com/linux/ubuntu/dists/bionic/pool/nightly/amd64/
   
   sudo dpkg -i 包
   ```

   ```
   1.创建docker组：sudo groupadd docker
   
   2.将当前用户加入docker组：sudo gpasswd -a ${USER} docker
   
   3.重启服务：sudo service docker restart
   
   4.刷新docker成员：newgrp - docker
   ```

   

   

   
