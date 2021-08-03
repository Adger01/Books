## privoxy简介
Privoxy是一款带过滤功能的代理服务器，针对HTTP、HTTPS协议，经常跟Tor组合使用。通过Privoxy的超级过滤功能，用户从而可以保护隐私、对网页内容进行过滤、管理cookies，以及拦阻各种广告等。

privoxy可以用作单机，也可以应用到多用户的网络，privoxy可以把SOCKS5转换为HTTP代理，也就是俗称的APN。

## 安装依赖

```
yum -y install make gcc 
yum  -y intall autoconf 
yum -y install zlib  zlib-devel
```

## 安装privoxy

```
去下载privoxy-3.0.8-stable-src.tar.gz
cd /data/src
wget http://www.privoxy.org/sf-download-mirror/Sources/3.0.8%20%28stable%29/privoxy-3.0.8-stable-src.tar.gz
tar xvf privoxy-3.0.8-stable-src.tar.gz
cd privoxy-3.0.8-stable-src
./configure --prefix=/opt/iapps/ss
make
make install
```

# 配置Privoxy

vim /opt/iapps/ss/etc/config

```
xxxxxxxxxx listen-address 127.0.0.1:8118   # 8118 是默认端口，不用改，下面会用到，如果要给局域网其他代理用，需要修改为0.0.0.0:8118forward-socks4a   /  127.0.0.1:9050 .  # 这里的端口写 shadowsocks 的本地端口（注意最后那个 . 不要漏了）
```

# 启动Privoxy

vim  /etc/systemd/system/privoxy.service

```
[Unit]

Description=Privoxy Web Proxy With Advanced Filtering Capabilities

Wants=network-online.target

After=network-online.target

[Service]

Type=forking

PIDFile=/opt/iapps/ss/etc/privoxy.pid

ExecStart=/opt/iapps/ss/sbin/privoxy --pidfile /opt/iapps/ss/etc/privoxy.pid --user privoxy  /opt/iapps/ss/etc/config

[Install]

WantedBy=multi-user.target

```

```
查看privoxy状态

# systemctl daemon-reload

# systemctl enable privoxy

# systemctl start privoxy

# systemctl status  privoxy
```

# 放开相关端口

**如果要给局域网内其他机器做代理用，配置文件中 listen-address 设置为 0.0.0.0:8118，需要放行！**

\# firewall-cmd –permanent –add-port=8118/tcp

\# firewall-cmd –reload

## 开启系统代理

```
vim /etc/profile
```

添加以下语句：

```
export http_proxy=http://127.0.0.1:8118       #这里的端口和上面 privoxy 中的保持一致
export https_proxy=http://127.0.0.1:8118
```

执行以下命令，使配置文件生效：

```
source /etc/profile
```



# 测试生效方法

```
curl -I www.google.com  #返回状态码为200，则表示成功
curl www.google.com   #返回一大堆html，则表示成功
```

