# owasp juice shop


# 使用Docker@Ubuntu16.04 LTS 64-bit來建置owasp juice shop

>* https://blog.gtwang.org/virtualization/ubuntu-linux-install-docker-tutorial/
```
Step 1:安裝Ubuntu16.04 LTS 64-bit

Step 2:在Ubuntu安裝 docker環境
sudo apt-get install docker.io

>* 查看docker 服務是否有正常啟動==>service docker status
>* 將自己的使用者帳號加入至 docker 群組==>sudo usermod -aG docker ksu
>* 登出再重新登入之後，就可以開始使用 Docker
>* 查看 Docker 的版本資訊==> docker version

Step 3:搜尋owasp juice shop的docker container image
docker search owasp juice shop

https://hub.docker.com/r/bkimminich/juice-shop/

Step 4:在 docker 環境上跑 juice shop

[1]下載docker container image
docker pull bkimminich/juice-shop

[2]啟動
docker run -d -p 3000:3000 bkimminich/juice-shop

Step 5:打開瀏覽器進行測試

   瀏覽 http://1.1.1.1:3000

所有的練習題都可以在 http://1.1.1.1:3000/#/score-board 上面看到/進度
```
# 使用Docker@Centos來建置owasp juice shop
```
Step 1:安裝 centos7

Step 2:在centos7安裝 docker環境
 yum install docker -y

Step 3:啟動 docker
systemctl start docker

Step 4:在 docker 環境上跑 juice shop

[1]下載docker container image
docker pull bkimminich/juice-shop

[2]啟動
docker run -d -p 3000:3000 bkimminich/juice-shop

Step 5:打開瀏覽器進行測試

   瀏覽 http://1.1.1.1:3000

所有的練習題都可以在 http://1.1.1.1:3000/#/score-board 上面看到/進度
```
 
參考資料
>* http://www.freebuf.com/sectool/151920.html
>* http://www.freebuf.com/column/152948.html

# 實戰owasp juice shop

>* [參考解答Pwning OWASP Juice Shop](https://leanpub.com/juice-shop)

