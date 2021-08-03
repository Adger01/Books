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

