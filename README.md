
# spider

&nbsp;&nbsp;使用`golang`写的爬取磁力链程序，将爬取到的数据存储到`MySQL`数据库中，差不多每秒钟能爬取到1至3条数据

### 使用方法

- 安装数据库

```shell
yum makecache fast
yum install mariadb-server mariadb
```

- 启动数据库

```shell
systemctl start mariadb
```

- 登陆创建存储数据的库

```sql
CREATE DATABASE dht CHARSET utf8mb4;
```

- 授权给`spider`程序连接数据库的用户

```sql
GRANT ALL PRIVILEGES ON dht.* TO 'btlet'@'127.0.0.1' IDENTIFIED BY 'PASSWORD';
```

- 创建存储数据的表

```sql
CREATE TABLE `dht_infohash` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `infohash` varchar(255),
  `name` text,
  `files` text,
  `hits` int(12) DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

> 如果爬取到的数据中某一字段超过数据库表中所定义字段长度，则程序会异常退出，可适当调整字段长度

### 运行程序

- 下载程序

```shell
git clone git@github.com:lulunalan/go-spider.git
cd go-spider
```

- 查看帮助

```shell
./spider --help
```

- 前台运行

```shell
./spider -p PASSWORD
```

- 后台运行

```shell
nohup ./spider -p PASSWORD &
```
