# Dockerfile-lnmp-redis-memcache




### 设置Docker镜像，加速下载

Mac下：

```
boot2docker ssh
sudo vi /var/lib/boot2docker/profile
EXTRA_ARGS="--registry-mirror=http://192.168.11.180:5000"
boot2docker restart
```

Ubuntu下:

```
vi /etc/default/docker
DOCKER_OPTS=" --registry-mirror http://192.168.11.180:5000 --insecure-registry 192.168.11.180:5000"
service docker restart
```

## 准备


- /var/www/data   存放MySQL数据库，Elastic数据
- /var/www/log    存放所有输出Log

创建这些目录:

```
mkdir /var/www /var/www/data /var/www/data/mysql /var/www/log /var/www/log/nginx /var/www/log/php
```

下载扩展配置文件

```
make dl
```

构建及运行环境

```
docker-compose build
docker-compose up
```