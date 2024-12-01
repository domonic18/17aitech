## 项目说明

📝 这个项目是一个基于 Docker 和 Apache 的 WordPress 环境配置。通过Docker Compose可以快速部署一个WordPress。

目的是提供一个安全且可扩展的 WordPress 开发和生产环境。


## 项目结构

```
.
├── apache
│   └── Dockerfile              # 构建wordpress镜像
│   └── apache.conf             # apache配置文件
├── docker-compose.yaml         # docker-compose配置文件
├── mysql_data                 # mysql数据目录
├── wordpress_data             # wordpress数据目录
├── ssl                        # ssl证书目录
```

## 使用方法
1. 安装docker
```bash
# 更新apt包索引
sudo apt-get update
# 安装docker
sudo apt-get install docker.io
```

2. 安装docker-compose
```bash
#下载docker-compose文件
curl -L https://github.com/docker/compose/releases/download/1.21.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

#将文件复制到/usr/local/bin环境变量下面
mv docker-compose /usr/local/bin

#给他一个执行权限
chmod +x /usr/local/bin/docker-compose

#查看是否安装成功
docker-compose -version
```

3. 修改docker的镜像源为国内
```json
# 编辑docker的daemon.json文件
sudo vim /etc/docker/daemon.json

# 添加以下内容
{
    "registry-mirrors": [
    "https://mirrors.tuna.tsinghua.edu.cn/dockerhub",
    "https://mirror.ccs.tencentyun.com/",
    "https://cr.console.aliyun.com",
    "http://hub-mirror.c.163.com"
  ]
}

```

4. 配置证书
将证书上传至工程目录下的 `ssl` 目录下,证书的构成一般是：
```
xxxx.com.crt
xxxx.com.key
root_bundle.crt
```
> 证书需要提前申请准备好，可以在阿里云或者腾讯云申请。

5. 配置环境变量
在工程目录下创建.env文件，并添加以下内容：
```bash
MYSQL_ROOT_PASSWORD=your_password
MYSQL_DATABASE=wordpress_db
MYSQL_USER=wpadmin
MYSQL_PASSWORD=your_password
WORDPRESS_DB_HOST=wp_mysql
WORDPRESS_DB_USER=wpadmin
WORDPRESS_DB_PASSWORD=your_password
WORDPRESS_DB_NAME=wordpress_db

```

6. 运行项目
```bash
docker-compose up -d
```


## 注意事项
1. 如果提示php.ini中upload_max_filesize限制大小。
解决方法：
```bash
# 编辑.htaccess文件
sudo vim /var/www/html/.htaccess

# 在.htaccess文件中添加以下内容
php_value upload_max_filesize 100M
php_value post_max_size 100M
```
