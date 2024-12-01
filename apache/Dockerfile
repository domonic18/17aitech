FROM wordpress:6.7.0-php8.3-apache

# 启用 Apache SSL 模块
RUN apt-get update && \
    apt-get install -y apache2 && \
    a2enmod ssl && \
    a2ensite default-ssl


# 设置工作目录
WORKDIR /var/www/html

# 复制 Apache 配置文件到容器中（如果有的话）
COPY apache-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# 暴露端口
EXPOSE 80
EXPOSE 443

