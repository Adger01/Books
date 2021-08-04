## 查看原有的内核

```
uname -a
Linux iZ2ze1ylmg1jee1gpwbp8uZ 4.18.0-305.3.1.el8.x86_64 #1 SMP Tue Jun 1 16:14:33 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux

cat /etc/redhat-release
CentOS Linux release 8.4.2105
centos版本号
```

### 更新仓库

```
yum -y update
```

### 启用 ELRepo 仓库



```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
yum install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
安装内核
yum --enablerepo=elrepo-kernel install kernel-ml

列出已安装的内核版本列表
rpm -qa | grep kernel

reboot



```



