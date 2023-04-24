# 使用python:3.9-slim-buster作為base image

首先建立一個名為bdse29app的資料夾，用以放置Dockerfile文件與專題資料。

開啟命令題字元，輸入wsl進入Windows的Linux虛擬主機。WSL (Windows Subsystem for Linux) 它是一個適用於Linux的Windows子系統

輸入cd /mnt/c/Users/XXX/bdse29app，進入Dockerfile所在的目錄中，
輸入docker image build -t bdse29appimage4 -f ./Dockerfile.txt .

這串指令是透過自製的Dockerfile來建置自己的映像檔bdse29appimage4 。

輸入docker container run -dit --name bdse29test4 -p 8085:5000 bdse29appimage4
-d：參數表示啟動一個後台執行的容器，也就是說容器會在背景執行而不會顯示 log 訊息在終端機上。
-i：參數表示開啟標準輸入（stdin），讓使用者可以跟容器互動。
-t：參數表示開啟一個伪终端（pseudo-TTY），這樣才能進行輸入輸出的互動操作。
-p 8085:5000：參數表示將主機的 8085 port 對應到容器的 5000 port，而我們的flask設定port=5000 ，讓瀏覽器可以透過 http://localhost:8085 訪問我們的網站。
