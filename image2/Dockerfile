# 使用httpd:2.4作為base image
FROM httpd:2.4

# 安裝python及其他必要套件
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
 && rm -rf /var/lib/apt/lists/*

# 複製app.py與template、static資料夾到容器中
COPY app.py /usr/local/apache2/htdocs/
COPY templates/ /usr/local/apache2/htdocs/templates/
COPY static/ /usr/local/apache2/htdocs/static/

# 安裝Flask及其他必要的python套件
RUN pip3 install Flask

# 複製httpd.conf到容器中，並加載MPM模組
COPY httpd.conf.txt /usr/local/apache2/conf/httpd.conf
RUN sed -i 's/#LoadModule mpm_event_module/LoadModule mpm_event_module/' /usr/local/apache2/conf/httpd.conf

# 暴露80端口
EXPOSE 80

# 啟動httpd及python Flask應用程式
CMD ["/bin/bash", "-c", "/usr/local/apache2/bin/httpd -DFOREGROUND & python3 /usr/local/apache2/htdocs/app.py"]
