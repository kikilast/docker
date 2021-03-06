# Docker 

個人學習筆記

## Docker basic introduction
docker建立在容器+虛擬化技術上

![alert tag](https://docs.docker.com/engine/images/engine-components-flow.png)

### 名詞解釋
- **Dockerfile** : 用來自動化建構映像檔的設定檔，內容就是包含所有建置映象所需要的指令

- **image** : 虛擬執行環境中硬碟資料的副本，算是運行虛擬環境的基礎，相對的虛擬環境地移轉也相當便利

- **container** : 基於映像運行的羽量級環境，也是Docker封裝和管理應用程式或微服務的環境

**關係圖**
![alert tag](https://qph.fs.quoracdn.net/main-qimg-9938910262ce5159df512e8baf5f8feb.webp)

  我認為Dockerfile就像是設定檔，根據設定檔建出映像，有點類似安裝光碟，根據這個安裝光碟，再建出一個容器，有點類似一台小電腦，而需要的服務就可以在這環境中運行

- **registry** : 儲存映像檔的地方，分為公有跟私有

- **repository** : 映像檔的集合，藉由*標籤*來區分版本

  [**Difference between Docker registry and repository**](https://stackoverflow.com/questions/34004076/difference-between-docker-registry-and-repository)

- **volume** : 資料卷，通常資料持久化的方法就是把它弄成檔案，但由於容器內部系統檔案的隔離，以及以沙盒模式運行的特性，對保存持久化的資料並不是很理想以及穩定，所以提供一種資料卷的方式將資料持久化保存在本地端

### Installation(以ubuntu為例)

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

登出之後再登入
指令前面就可以不用加`sudo`了

### Build

由Dockerfile建立映像檔

### Pull

取得映像檔

### run
運行映像檔 建立容器

### 

