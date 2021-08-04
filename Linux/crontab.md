## crontab引发的命案

使用`laravel`框架创建的`crontab`

```
* * * * * /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
```

造成的结果是一些自动生成的目录和日志文件都是`root`权限，原因是`crontab`是使用`root`用户执行的。

#### 2种解决方案

###### 方案1 （推荐）

```
指定www用户的crontab
sudo crontab -u www -e
* * * * * /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
```

方案2

```
sudo crontab -e
* * * * * www /path/to/php /path/to/artisan schedule:run >> /dev/null 2>&1
虽然这里指定了www用户，但是发现没有执行成功，查看日志的时候(tail -f /var/log/cron),发现www未找到。
解决办法
修改/etc/passwd ,把www用户的/usr/sbin/nologin改为/bin/bash
```

