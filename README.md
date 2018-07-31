# Docker 

## Docker basic concept


### install(以ubuntu為例)

Windows的部分 
因為底層的模式與Linux不同
所以無法直接使用
需要安裝額外的程式
[docker for windows](https://docs.docker.com/docker-for-windows/install/)

Linux的安裝套件中幾乎都有可以直接安裝docker的指令
可以直接call指令安裝

```cmd
sudo apt-get update
sudo appt-get install docker.io
```

安裝好之後
把自己加到有權限使用docker的群組裡面

```cmd
sudo usermod -aG docker $(whoami)
```

重新開機之後
指令前面就可以不用加`sudo`了

### pull



### run


### 

## Docker Registry
可以用來存放docker image的地方，分為公有和私有。公有的部分[Dockerhub](https://hub.docker.com), [Quay](https://quay.io)都是可以存放映像檔的地方，是可以公開存取的，直接把映像檔拉下來即可使用，私有的部分，目前三大雲服務都有提供放置映像檔的地方，*azure-azure container registry*, *aws-amazon elastic container registry*, *gcp-container registry*。另外也可以在本地端架設私有的存放庫。

### Pratice:
公、私有的docker registry 布建以及推送映像檔(以ubuntu為例)
#### 本地端(私有)
安裝docker
```cmd
sudo apt-get update
sudo apt-get install docker.io
```
在安裝好docker之後，以容器的形式來建立docker registry

```cmd
docker run -d -p 5000:5000 --restart=always --name registry \
-v $(pwd)/data:/var/lib/registry \
registry:2
```

> -v 為 host 與 container 要進行同步的目錄，主要存放 docker images 資料

可以在部屬一個容器 docker registry UI 來方便檢視映像檔
```cmd
docker run -d -p 5001:80 \
-e ENV_DOCKER_REGISTRY_HOST={HOST IP} \
-e ENV_DOCKER_REGISTRY_PORT=5000 \
konradkleine/docker-registry-frontend:v2
```

可以瀏覽器進入UI來觀察

> http://localhost:5001

將映像檔推上本地端的registry
如果沒有可以先拉一個公開的映像檔下來

```cmd
docker pull mysql
```

標記自己的映像檔
```cmd
docker tag mysql localhost:5000/mysql
```

將localhost:5000/mysql推上本地端的registry

```cmd
docker push localhost:5000/mysql
```

再去UI上確認，就會多一個repository

無法刪除單一映像檔，只能將整個repository刪除或是刪除標籤

#### 雲端(公有 dockerhub)
登入 container registry
```cmd
az acr login --name mygistry
```
或是
```cmd
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
  ```
  
在將映像推送至您的登錄之前，必須使用 ACR 登入伺服器名稱來標記映像。 使用 docker tag 命令來標記映像。 將登入伺服器取代為您先前記錄的登入伺服器名稱。
```cmd
docker tag <image repository name> <login server>/<image name>:<version>
```

單純把image 推上dockerhub
```cmd
docker push <username>/<repo name>:<Tag name>
```
最後把image推送上container registry
```cmd
docker push <login server>/<repo name>:<Tag name>
```
