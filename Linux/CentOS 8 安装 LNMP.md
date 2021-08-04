# 创建halo_op用户
创建用户，并且赋予sudo权限
```shell
创建用户组
groupadd halo_op
创建用户，并添加到用户组，并生成家目录
useradd -g halo_op halo_op -m
cd到新用户的家目录
cd /home/halo_op
切换到新用户
su halo_op
修改权限
chmod +w /etc/sudoers
vi /etc/sudoers
最后一行加上
halo_op ALL=(ALL) NOPASSWD: ALL
chmod -w /etc/sudoers

使用root的用户修改密码
passwd halo_op
从halo_op切换到root用户
sudo -s
```

## 安装MySQL

### 创建用户

```
groupadd mysql
useradd -g mysql mysql
```

### 创建db存储的文件夹

```
mkdir -p /data/db/mysql8
```

### 下载mysql并安装

```
cd /data/src
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.26.tar.gz
tar xvf mysql-8.0.26.tar.gz

mkdir build && cd build



sudo yum install -y bison bzip2 git hostname ncurses-devel openssl openssl-devel pkgconfig tar wget zlib-devel doxygen diffutils rpcgen make libtirpc-devel

dnf --enablerepo=powertools install doxygen
dnf --enablerepo=powertools install rpcgen

cmake .. \
-DDOWNLOAD_BOOST=1 \
-DWITH_BOOST=. \
-DDEFAULT_CHARSET=utf8mb4 \
-DDEFAULT_COLLATION=utf8mb4_unicode_ci \
-DENABLED_LOCAL_INFILE=ON \
-DWITH_SSL=system \
-DCMAKE_INSTALL_PREFIX=/opt/iapps/mysql/mysql8 \
-DMYSQL_DATADIR=/data/db/mysql/mysql8/data \
-DMYSQL_TCP_PORT=3306 -DFORCE_INSOURCE_BUILD=1

cd ../

make 
make install


```

