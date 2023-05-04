# Docker環境建制
我們的網站是由Docker來架設，首先先編寫一個Dockerfile。

Dockerfile是一種文本文件，其中包含了一個image的所有指令，從而讓Docker引擎可以自動構建一個包含所需應用程序的映像。也可以說它是一個使用container的說明書，依照環境與使用者需求編寫指令。

image與container 完成後，這一個完整的docker host就可以與其中的flask程式做溝通，以達成在本地端的瀏覽器上呈現我們的網站。

## 1.首先建立一個資料夾(website_v7)，用以放置Dockerfile文件、python flask程式與模型資料。

## 2.開啟命令題字元，輸入WSL進入Linux虛擬環境。WSL (Windows Subsystem for Linux) 它是一個適用於Linux的Windows子系統

## 3.cd /mnt/c/Users/XXX/website_v7，進入Dockerfile所在的目錄中

## 4.建立映像:

### -> docker image build -t bdse29image -f ./Dockerfile.txt .

-這串指令是透過Dockerfile來建置映像檔。docker引擎會按照dockerfile步驟自動建置映像。

## 5.建立Linux虛擬網路:

### -> docker network create bdse29network

## 6.建立主程式容器:

### -> docker container run -dit --name bdse29web -p 8082:5000 --network bdse29network bdse29image

-d：參數表示啟動一個後台執行的容器，也就是說容器會在背景執行而不會顯示 log 訊息在終端機上。

-i：參數表示開啟標準輸入（stdin），讓使用者可以跟容器互動。

-t：參數表示開啟一個偽終端（pseudo-TTY），這樣才能進行輸入輸出的互動操作。

-p 8082:5000：參數表示將主機的 8082 port 對應到容器的 5000 port，而我們的flask設定port=5000 ，讓瀏覽器可以透過 [http://localhost:8082](http://localhost:8082/) 訪問我們的網站。

--network：將容器放進虛擬網路中

## 7.登入並註冊ngrok網站，取得私人token
'<token>' = 個人token

## 8.建立ngrok容器:

### -> docker run -it --name bdses29ngrok -e NGROK_AUTHTOKEN=<token> --network bdse29network ngrok/ngrok http bdse29web:5000

-隨後ngrok容器就能連接到bdse29web容器中的網頁端口(5000)

