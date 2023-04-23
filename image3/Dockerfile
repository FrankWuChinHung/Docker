# 使用 httpd 映像檔作為基礎
FROM python:3.9-slim-buster

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apt-utils dpkg gnupg

# 安裝 Apache
RUN apt-get update && \
    apt-get install -y apache2

# 安裝 mod_wsgi
RUN apt-get install -y libapache2-mod-wsgi-py3

# 設定 Apache 的文件根目錄
ENV APACHE_DOCUMENT_ROOT=/var/www/html/myapp

# 將 Apache 設定檔中的 DocumentRoot 設為環境變數所指定的目錄
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
        && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# 將 Flask 程式碼複製到容器中的目錄
COPY app.py ${APACHE_DOCUMENT_ROOT}/
COPY templates/ ${APACHE_DOCUMENT_ROOT}/templates/
COPY static/ ${APACHE_DOCUMENT_ROOT}/static/
COPY app.wsgi.txt /var/www/html/

# 安裝 app.py 所需的 Python 套件
RUN pip install flask
RUN pip install gunicorn

# 複製 httpd.conf 文件到 Apache 的配置目錄
COPY httpd.conf.txt /etc/apache2/httpd.conf

# 啟用 Apache 的 rewrite 和 wsgi 模組
RUN a2enmod rewrite && \
    a2enmod wsgi

# 啟動 Apache
CMD ["python3", "/var/www/html/myapp/app.py"]
