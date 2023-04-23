# 安裝python及其他必要套件
RUN apt-get update \
 && apt-get install -y \
    python3 \
    python3-pip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# 複製app.py與template、static資料夾到容器中
COPY app.py /usr/local/apache2/htdocs/
COPY templates/ /usr/local/apache2/htdocs/templates/
COPY static/ /usr/local/apache2/htdocs/static/

# 安裝Flask及其他必要的python套件
RUN pip3 install Flask

# 將httpd.conf複製到容器中，並啟用mod_proxy及mod_proxy_http模組
COPY httpd.conf.txt /usr/local/apache2/conf/httpd.conf.txt


# 暴露80端口
EXPOSE 80

# 啟動python Flask應用程式及httpd
CMD ["/bin/bash", "-c", "python3 /usr/local/apache2/htdocs/app.py & /usr/local/apache2/bin/httpd -DFOREGROUND"]
