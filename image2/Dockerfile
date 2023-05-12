# 使用Python3.9作為映像檔來源
FROM python:3.9-slim-buster

# 複製Flask應用程式代碼到容器中
WORKDIR /app
COPY app.py .
COPY templates/ templates/
COPY static/ static/
COPY model/ model/
COPY data/ data/

# 安裝Flask和其他必要的Python套件
RUN pip install --upgrade pip && \
    pip install flask && \
    pip install pandas && \
    pip install joblib && \
    pip install xgboost && \
    pip install Scikit-Learn --upgrade
    

CMD [ "python", "./app.py" ]
