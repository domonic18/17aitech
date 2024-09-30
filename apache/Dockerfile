FROM wordpress:latest

# 启用 Apache SSL 模块
RUN apt-get update && \
    apt-get install -y apache2 && \
    a2enmod ssl && \
    a2ensite default-ssl

# 复制自定义的 SSL 配置文件
COPY ./apache/apache-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# 复制 SSL 证书
COPY ./ssl /etc/apache2/ssl

# 重新启动 Apache
CMD ["apachectl", "-D", "FOREGROUND"]
