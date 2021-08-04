## crontab的级别

`crontab`分为2个级别，用户级别和系统级别

用户级别的使用方式(-e编辑的真实文件都在/var/spool/cron下)

```
crontab -e
sudo crontab -e
sudo crontab -u www -e
```

系统级别(系统级别的真实文件存在于/etc/crontab)

```
系统级别的crontab可以指定不同的用户
* * * * * www export APP_ENV=production && /path/to/php /path/to/project/artisan schedule:run >> /dev/null 2>&1
* * * * * root export APP_ENV=production && /path/to/php /path/to/project/artisan schedule:run >> /dev/null 2>&1
```



## Laravel中创建crontab

```
sudo crontab -u www -e
* * * * * export APP_ENV=production && /path/to/php /path/to/project/artisan schedule:run >> /dev/null 2>&1
```



## crontab引发的命案

使用`laravel`框架创建的`crontab`

```
* * * * * /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
```

造成的结果是一些自动生成的目录和日志文件都是`root`权限，原因是`crontab`是使用`root`用户执行的。

#### 2种解决方案

###### 方案1 

```
指定www用户的crontab
sudo crontab -u www -e
* * * * * /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
```

方案2（推荐）

```
sudo vim /etc/crontab
* * * * * www /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1

因为放在这里，可以统一管理用户。
```

禁止使用姿势

```
sudo crontab -e
* * * * * www /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
这里会把www当成一个命令看待。
```

