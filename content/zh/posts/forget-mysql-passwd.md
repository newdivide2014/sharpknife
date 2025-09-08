+++
title =  "mysql忘记密码的恢复方式"
author = "蓝红柿"
date = 2025-09-08T17:55:41+08:00
lastmod = 2021-09-08T17:55:41+08:00
draft = false
tags = ["Mysql"]
categories = ["Linux"]
+++
{{< badge >}}
新文章！
{{< /badge >}}
1.  停止mysql服务

<!--listend-->

```shell
/etc/init.d/mysql stop
```

2.  以不检查权限的方式启动mysql

<!--listend-->

```shell
mysqld --skip-grant-tables &
```

3.  用空密码方式使用root用户登录mysql

<!--listend-->

```shell
mysql -u root
```

4.  修改root用户的密码

<!--listend-->

```sql
mysql> update MySQL.user set password=PASSWORD('newpassword') where User='root';  # newpassword就是要设置的新的密码
mysql> flush privileges;
mysql> quit;
```

5.  重启mysql服务

<!--listend-->

```shell
/etc/init.d/mysql restart
```
