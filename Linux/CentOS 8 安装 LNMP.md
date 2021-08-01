# 创建halo_op用户
创建用户，并且赋予sudo权限
```shell
groupadd halo_op
useradd -g halo_op halo_op -m
cd /home/halo_op
su halo_op
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

